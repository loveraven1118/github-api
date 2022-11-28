<template>
    <div class="table">
        <table>
            <thead>
                <tr>
                    <th>Title</th>
                    <th>Info</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="content in theadContent" :key="content.title">
                    <td>{{ content.title }}</td>
                    <td>{{ content.info }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
const username = 'loveraven1118'
const repos = 'github-api'
const headers = new Headers()
headers.append('Accept', 'application/vnd.github.v3+json')
const config = {
  method: 'GET',
  headers: headers,
  redirect: 'follow'
}

export default ({
  name: 'DataDetailTable',
  data () {
    return {
      theadContent: []
    }
  },
  mounted: function () {
    this.getissue(this.$route.query.Id)
  },
  methods: {
    getissue: function (id) {
      const url = 'https://api.github.com/repos/' + username + '/' + repos + '/issues/' + id
      this.theadContent = []
      fetch(url, config).then(response => response.json())
        .then(result => {
          console.log(result)
          this.theadContent.push({
            title: 'Title',
            info: result.title
          })
          this.theadContent.push({
            title: 'State',
            info: result.state
          })
          this.theadContent.push({
            title: 'Content',
            info: result.body
          })
          this.theadContent.push({
            title: 'Create Date',
            info: result.created_at
          })
        })
        .catch(error => console.log('error', error))
    }
  }
})
</script>
