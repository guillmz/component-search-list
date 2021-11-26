<template>
  <div class="wrapper">
    <div
      class="text-wrapper mb-1"
      v-on:click="listShow"
      :style="{ cursor: 'pointer' }"
    >
      <div
        :style="{
          display: 'flex',
          justifyContent: 'center',
          alignItems: 'center',
          position: 'relative',
        }"
      >
        <p v-if="!this.valueSelect">Seleccione</p>
        <i
          class="far fa-angle-down"
          v-if="!isShowList"
          :style="{ position: 'absolute', right: 0 }"
        />

        <p v-if="this.valueSelect">
          {{ this.valueSelect }}
        </p>
        <i
          class="far fa-angle-up"
          v-if="isShowList"
          :style="{ position: 'absolute', right: 0 }"
        />
      </div>
    </div>

    <div v-if="isShowList">
      <input
        class="form-control"
        type="text"
        v-model="search"
        placeholder="Search"
      />
    </div>
  </div>
  <div class="table-wrapper" v-if="isShowList">
    <table v-if="dataList.length" class="table">
      <thead>
        <tr>
          <th>Nro</th>
          <th>Titulo</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="el in result"
          v-bind:key="el.title"
          v-on:click="listHidden(el.title)"
          :style="{ cursor: 'pointer' }"
        >
          <td>
            {{ el.nro }}
          </td>
          <td>
            {{ el.title }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "SearchList",
  data() {
    return {
      search: null,
      isShowList: false,
      valueSelect: "",
      dataList: [
        { title: "React", nro: "1" },
        { title: "Vue", nro: "2" },
        { title: "Angular", nro: "3" },
        { title: "Node", nro: "4" },
        { title: "PHP", nro: "5" },
      ],
    };
  },
  methods: {
    listShow: function () {
      this.isShowList = true;
    },
    listHidden: function (title) {
      this.isShowList = false;
      this.valueSelect = title;
      this.search = null;
    },
  },
  computed: {
    result() {
      if (this.search) {
        return this.dataList.filter((el) => {
          return Object.values(el)
            .join(" ")
            .toLowerCase()
            .match(this.search.toLowerCase());
        });
      } else {
        return this.dataList;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.wrapper,
.table-wrapper {
  width: 40%;
  margin: 0 auto;
}
input,
select,
.text-wrapper {
  height: 50px;
}
.text-wrapper {
  background-clip: padding-box;
  border: 1px solid #ced4da;
  border-radius: 0.25em;
  padding-right: 15px;
  padding-left: 15px;
}
.text-wrapper p {
  margin: 0.8em;
}
</style>
