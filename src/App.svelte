<script lang="ts">
  import Profile from "./Profile.svelte";
  import Todos from "./Todos.svelte";
  import { onMount } from "svelte";
  import { auth, googleProvider } from "./services/firebase";
  import { authState } from "rxfire/auth";

  let user;
  const unsubscribe = authState(auth).subscribe((u) => (user = u));
  function login() {
    auth.signInWithPopup(googleProvider);
  }

  onMount(async () => {
    console.log("aaaaaaaaa");
  });
</script>

<section>
  {#if user}
    <Profile {...user} />
    <button on:click={() => auth.signOut()}>Logout</button>
    <hr />
    <Todos uid={user.uid} />
  {:else}
    <button on:click={login}> Signin with Google </button>
  {/if}
</section>
