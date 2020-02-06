<template>
    <header>
      <p><b>Academy</b></p>
        <div class="nav">
          <ul>
            <li><a href="#">Lecture</a></li>
            <li><a class="active" href="#">Videos</a></li>
          </ul>
        </div>
      </header>
</template>

<style>
header {
  box-sizing: border-box;
  margin-bottom: 20px;
}

li, a, p {
  font-family: "Montserrat", sans-serif;
  font-weight: 500;
  font-size: 16px;
  color: #edf0f1;
  text-decoration: none;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px 10%;
}

.nav {
  list-style: none;
}

.nav li {
  display: inline-block;
  padding: 0px 20px;
}

.nav li a {
  transition: all 0.3s ease 0s;
}

.nav li a:hover {
  color:gray
}
</style>