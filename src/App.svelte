<script>
  let placeholder = "set your intention";
  let title;
  const updateTitle = () => {
    if (title.length > 0) {
      window.electronAPI.setTitle(title);
    }
  };
  const hideWindow = () => {
    windowClosedReset();
    window.electronAPI.toggleWindow();
  };
  window.electronAPI.onAppBlurred(() => {
    windowClosedReset();
  });
  const windowClosedReset = () => {
    if (title.length > 0) {
      placeholder = title;
      title = "";
    }
  };
  const setTitleAndHideWindow = () => {
    updateTitle();
    hideWindow();
  };

  const iconPath = "./focus.png";
</script>

<main style="text-align:center; display:flex; flex-direction: column; justify-content: center; align-items: center; height: 100vh;">
  <div>
    <form on:submit|preventDefault>
      <div style="display:flex; justify-content: center; align-items: center;">
        <img style="margin-right: 10px;" height="26" src={iconPath} alt="Intentions app logo" />
        <input autofocus class="intention-input" type="text" bind:value={title} {placeholder} on:keyup={updateTitle} />
      </div>
      <div style="display:none; margin-top: 10px;"><button on:click={setTitleAndHideWindow}>Update</button></div>
    </form>
  </div>
</main>

<style>
  main {
    font-family: "Quicksand", sans-serif;
    font-weight: 300;
    margin: 0;
    padding: 0;
  }
  form {
    margin: 0;
    padding: 0;
  }
  input {
    margin: 0;
    outline-color: #ae90da;
    outline-width: 10px;
  }
  .intention-input {
    width: 300px;
    text-align: center;
  }
</style>
