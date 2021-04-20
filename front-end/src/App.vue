<template>
  <div id="app">
    <header id="header">
      <h1 class="webtitle">Booksy</h1>
      <nav>
        <router-link to="/"><i class="fas fa-home"></i></router-link>
        <router-link to="/dashboard"><i class="fas fa-user"></i></router-link>
      </nav>
    </header>
    <router-view />

    <div class='footer'>
      <a href = 'https://github.com/chapkirsten/final'>13 Hours. https://github.com/chapkirsten/final</a>
    </div>
  </div>
</template>

<style>

body {
  font-family: 'Work Sans', sans-serif;
  font-weight: 300;
  font-size: 13pt;
  margin: 0px 200px;
}
#header {

  margin: 0 1em 1em 0;
  height: 175px;
  width: 100%;
  position: fixed;
  z-index: 10000;
  left: 50%;
  transform: translate(-50%, 0);
  background: #457373;
  text-align: center;
  box-shadow: 0 0 0 1em #FFF;
}
.webtitle{
  font-size: 50px;
  font-family: didot, serif;
}
nav {
  display: flex;
  justify-content: center;
}
h1 {
  color: #fff;
  font-size: 18px;
}
h2 {
  font-size: 12px;
}
#header .fas {
  font-size: 25px;
  color: #fff;
  width: 50px;
}
.pure-button-primary {
  background-color: #277E8E;
}

.footer{
  position:fixed;
  left: 0;
  bottom: 0;
  background-color: #D9C179;
  color: white;
  text-align: center;
  width: 100%;
}

a{
  color: white;
}
</style>
