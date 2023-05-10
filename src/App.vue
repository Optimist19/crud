<template>
  <!-- <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/edit">About</router-link>
  </nav> -->
  <router-view/>
</template>

<style>

.form-btn{
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 2vh;
}


.modal{
  position: fixed;
  height: 100%;
  width: 100%;
  background-color: rgba(209, 255, 182, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
}

p, input{
  margin: 0 1vw 0 1vw;
  padding: 1.5vh 0;
}

input{
  width: 25vw;
}

input::placeholder{
  padding-left: 4px;
  font-size: 18px;
}


.modal-con{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: white;
  max-width: 30%;
  height: 60%;
}

.close-btn{
  position: absolute;
  top: 21vh;
  right: 37vw;
}

.close-btn button{
  font-size: 29px;
  border: none;
  background-color: white;
  cursor: pointer;
}
</style>
