<template>
  <div id="app">
    <div class="jumbotron">
      <div class="container">
        <h1>faApps Frontend Demo</h1>
        <p>This is a simple vueJs demo running one descentralized node.</p>
        <p>
          To be a node, get
          <a
            target="_blank"
            href="https://github.com/fdapps-tools/backend#setup"
            >project repository</a
          >
          and run project with setup NETWORK_NODE_URL={{ link }}
        </p>
      </div>
    </div>

    <div class="container">
      <h2>Active Nodes</h2>
      <table class="table table-condensed">
        <thead>
          <tr>
            <th>Address</th>
            <th>Last Check</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(node, index) in nodes" :key="index">
            <td>{{ node.host }}</td>
            <td>{{ node.lastcheck }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      link: location.href,
      nodes: [],
    };
  },

  async beforeMount() {
    const nodes = await this.getNodeList();
    this.nodes = nodes;
  },

  methods: {
    getNodeList() {
      return new Promise((resolve, reject) => {
        fetch(`${this.link}/nodes`)
          .then((response) => {
            if (response.status === 200) {
              resolve(response.json());
            } else {
              reject(response);
            }
          })
          .catch((err) => {
            reject(err);
          });
      });
    },
  },
};
</script>

<style>
</style>
