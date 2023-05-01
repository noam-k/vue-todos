<template>
  <div class="about">
    <h1>Todo App using VueJS</h1>
  </div>
  <p>
    Hi, my name is Noam Kritenberg and I built this application in order to 
    learn the basics of VueJS.
  </p>
  <p>
     Special thanks to <a href="https://www.johnkomarnicki.com/"> John
     Komarnicki </a> for creating lots of VueJS content, I learned a lot from
     his content.
  </p> 
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
h1, p {
    padding: 8px;
}
</style>
