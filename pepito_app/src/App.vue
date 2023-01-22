<template>
  <div class="navBar h-16 px-4 flex justify-between items-center bg-cyan-400">
    <!--logo-->
    <div class="logo">
      <router-link to="/">
          <p>LOGO</p>
      </router-link>
    </div>
    <!--menu-->
    <div class="menu flex gap-4">
      <router-link to="/profile">
        <p>Profile</p>
      </router-link>
      <router-link to="/chat">
        <p>Chat</p>
      </router-link>
    </div>
  </div>
  <router-view/>
</template>


