<template>
  <div class="table">
    <button @click="getdatas(1)">click</button>
    <table>
      <thead>
        <tr>
          <th>Issue Number</th>
          <th>Issue Title</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="content in theadContent" :key="content.number">
          <td>{{ content.number }}</td>
          <td>{{ content.title }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
const pagesize = 10
const username = 'loveraven1118'
const repos = 'github-api'
const headers = new Headers()
headers.append('Accept', 'application/vnd.github.v3+json')
const config = {
  method: 'GET',
  headers: headers,
  redirect: 'follow'
}

export default {
  name: 'DataTable',
  data () {
    return {
      theadContent: []
    }
  },
  mounted: function () {
    this.getdatas(1)
  },
  methods: {
    getdatas: function (page) {
      const url = 'https://api.github.com/repos/' + username + '/' + repos + '/issues?per_page=' + pagesize + '&page=' + page
      this.theadContent = []
      fetch(url, config).then(response => response.json())
        .then(result => {
          for (var i = 0; i < result.length; i++) {
            this.theadContent.push({
              number: result[i].number,
              title: result[i].title
            })
          }
        })
        .catch(error => console.log('error', error))
    }
  }
}
</script>
