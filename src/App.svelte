<script>
  import Modal from "./Modal.svelte";
  import AddPeopleForm from "./AddPeopleForm.svelte";
  let name = "Dimitris";
  let invitees = [];
  let inputSurname;
  let id = 1;
  let firstName = "";
  let lastName = "";
  let showModal = true;

  const addToArray = (e) => {
    if (firstName != "" && lastName != "") {
      invitees = [
        ...invitees,
        { id: id++, Surname: lastName, Name: firstName },
      ];
      console.table(invitees);
      firstName = "";
      lastName = "";
      inputSurname.focus();
    } else {
      console.error("Both inputs should be filled");
    }
  };

  const checkEnter = (e) => {
    if (e.keyCode === 13) {
      addToArray();
    }
  };

  const clear = () => {
    invitees = [];
    id = 1;
    firstName = "";
    lastName = "";
    console.clear();
  };

  const deleteInv = (id) => {
    invitees = invitees.filter((invitee) => invitee.id != id);
    console.table(invitees);
  };

  const toggleModal = () => {
    showModal = !showModal;
  };
</script>

<!-- <Modal message="try again." isSuccessModal={false} /> -->
<Modal isSuccessModal={true} {showModal} on:click={toggleModal}>
  <h3>Hello {name}, from yesterday</h3>
  <AddPeopleForm />
</Modal>
<main>
  <h1>Hello {name}!</h1>
  <h3>Welcome to #webflow Party!</h3>
  <h4>Enter the details of each invitee</h4>
  <div>
    <input
      type="text"
      placeholder="Surname"
      bind:value={lastName}
      bind:this={inputSurname}
      on:keydown={checkEnter}
    />
    <input
      type="text"
      id="name"
      placeholder="Name"
      bind:value={firstName}
      on:keydown={checkEnter}
    />

    <button on:click={addToArray}>Add</button>
    <button on:click={clear}>Clear</button>
  </div>
  <div class="list">
    {#each invitees as invitee (invitee.id)}
      <!-- (invitee.id) ^^? -->
      <div class="invitee">
        <p>
          {invitee.Surname.charAt(0).toUpperCase() + invitee.Surname.slice(1)} -
          {invitee.Name.charAt(0).toUpperCase() + invitee.Name.slice(1)}
        </p>
        {#if invitee.Surname === "theofanous" || invitee.Surname === "Theofanous"}
          <p style="color:red">&nbsp; TITAN!!</p>
        {/if}
        <button
          class="delete"
          on:click={() => {
            deleteInv(invitee.id);
          }}>Delete</button
        >
      </div>
    {:else}
      <p>There are no people to show..</p>
    {/each}
  </div>
  <strong>Total invitees: {invitees.length}</strong>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  .list {
    margin-bottom: 20px;
  }

  .delete {
    margin-left: 1rem;
    font-size: 12px;
  }

  .invitee {
    display: flex;
    justify-content: center;
    align-items: baseline;
    padding: 0.22rem;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
