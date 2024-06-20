<template>
  <div>
    <header class="header">
      <nav class="menu">
        <ul>
          <li><router-link to="/">Home</router-link></li>
          <li><router-link to="/todos">Todos</router-link></li>
          <li><router-link to="/posts">Posts</router-link></li>
          <li><router-link to="/albums">Albums</router-link></li>
          <li><router-link to="/about">About</router-link></li>
        </ul>
      </nav>
    </header>
    <router-view></router-view>
  </div>
</template>

<style>
.header {
  background-color: #1e1e1e;
  padding: 15px 0;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  position: fixed;
  width: 100%;
  top: 0;
  z-index: 1000;
}

.menu {
  max-width: 1200px;
  margin: 0 auto;
}

.menu ul {
  display: flex;
  justify-content: center;
  list-style: none;
  padding: 0;
  margin: 0;
}

.menu ul li {
  margin: 0 20px;
}

.menu ul li a {
  text-decoration: none;
  color: #ffffff;
  font-weight: 600;
  font-size: 18px;
  padding: 10px 15px;
  border-radius: 5px;
  transition: background-color 0.3s, transform 0.3s;
}

.menu ul li a:hover {
  background-color: #ff6600;
  color: #ffffff;
  transform: translateY(-3px);
}

.menu ul li a.router-link-exact-active {
  background-color: #ff6600;
  color: #ffffff;
  transform: scale(1.05);
}
</style>
