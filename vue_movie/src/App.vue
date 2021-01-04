<template>
  <header>
    <router-link to="/">
    <h1><span>vue</span>movies</h1>
    </router-link>
  </header>
  <main>
  <router-view/>

  </main>
  
</template>

<style lang="scss">
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;

  &::selection{
    background: transparentize(#709055, 0.5);
  }
}

body{
  background-color: teal;
}

a {
  text-decoration: none;
}

header{
  display :  flex;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: salmon;
  box-shadow: 0 0 6px rgba(0,0,0,0.3);

  h1 {
    color: whitesmoke;
    font-size: 25px;

    span{
      color: crimson;
    }
  }
}
</style>
