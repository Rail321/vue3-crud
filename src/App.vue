<template>
  <div>
    <ul>
      <li>
        <router-link to="/">Home</router-link>
      </li>
      
      <li>
        <router-link to="/posts">Posts</router-link>
      </li>
    </ul>
    
    <router-view />
  </div>
</template>