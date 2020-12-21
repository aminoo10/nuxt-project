<template>
  <div>
    <Header :show= false :query="``"/>
    <Nuxt />
  </div>
</template>

<style lang="scss">
html {
  font-family:
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}

.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;

  &:hover {
    color: #fff;
    background-color: #3b8070;
  }
}

.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #35495e;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;

  &:hover {
    color: #fff;
    background-color: #35495e;
  }
}

.button--red {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #9e1a1a;
  color: #9e1a1a;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;

  &:hover {
    color: #fff;
    background-color: #9e1a1a;
  }
}

//I wanted to define container here but it kinda broke a bunch of stuff on the 'results' page for some reason, figure I just don't mess with it...
// .container {
//   margin: 0 auto;
//   min-height: 100vh;
//   display: flex;
//   flex-direction: column;
//   justify-content: center;
//   align-items: center;
//   text-align: center;
// }


</style>
