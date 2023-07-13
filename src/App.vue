<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light mb-3">
      <div class="container">
        <a class="navbar-brand" href="/">MAPS MARKER</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
          aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ml-auto">
              <li class="nav-item">
                <RouterLink to="/firstTask" class="nav-link">Task 1</RouterLink>
              </li>
            <li class="nav-item">
              <RouterLink to="/secondTask" class="nav-link">Task 2</RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink to="/thirdTask" class="nav-link">Task 3</RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink to="/fourthTask" class="nav-link">Task 4</RouterLink>
            </li>
            <li class="nav-item">
              <RouterLink to="/fifthTask" class="nav-link">Task 5</RouterLink>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <RouterView />
     <div class="map-container">
        <!-- Your map code or component here -->
      </div>
  </div>
</template>

<style scoped>
header {
  padding-top: 20px;
  padding-bottom: 20px;
}

.navbar-brand {
  font-size: 30px;
  font-weight: bold;
}

.navbar-nav .nav-link {
  font-size: 25px;
  font: 2rem sans-serif;
}

.map-container {
  margin-top: 20px;
  padding: 200px;
  width:100vh;
}

@media (max-width: 991.98px) {
  .navbar-nav.ml-auto {
    margin-top: 10px;
  }
}
</style>