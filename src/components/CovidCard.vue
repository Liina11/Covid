<template>
  <div class="card">
      <header class="card-header">
          <p class="card-header-title">
              <router-link :to="'/covid/' + country.Slug" >{{country.Country}}</router-link>
          </p>
      </header>
      <div class="card-content">
          <div class="content">
              <table class="table is-striped is-hoverable">
                  <tbody>
                      <tr>
                          <th>Total Confirmed:</th>
                          <td>{{country.TotalConfirmed}}</td>
                      </tr>
                      <tr>
                          <th>Total Deaths:</th>
                          <td>{{country.TotalDeaths}}</td>
                      </tr>
                      
                      <tr>
                          <th>New Confirmed:</th>
                          <td>{{country.NewConfirmed}}</td>
                      </tr>
                      <tr>
                          <th>New Deaths:</th>
                          <td>{{country.NewDeaths}}</td>
                      </tr>
                     
                  </tbody>
              </table>
          </div>
      </div>
  </div>
</template>

<script>
export default {
    props: ['country']
}
</script>

<style>
</style>