<script>
  import Quizzes from "./Quizzes.svelte";
  import Game from "./Game.svelte";
  import Create from "./Create.svelte";

  //let state = "quizzes";
  let state = "quizzes";
  let quiz;

  function handleMessage(event) {
    state = "host_game";
    quiz = event.detail.quiz;
  }

  function state_change(event) {
    state = "quizzes";
  }
</script>

<div id="main" class="block">
  {#if state == "quizzes"}
    <h1 class="block">Select a Quiz</h1>
    <Quizzes on:select_quiz={handleMessage} />
    <button class="button" on:click={() => (state = "create_quiz")}
      >Create New Quiz</button
    >
  {/if}
  {#if state == "host_game"}
    <Game {quiz} />
  {/if}
  {#if state == "create_quiz"}
    <Create on:quizzes={state_change} />
  {/if}
</div>

<style>
  #main {
    padding: 10%;
  }
</style>
