<template>

  <section class="src-components-table-users">
    <div class="jumbotron">
      <table class="table">
        <thead>
          <th>Nombre</th>
          <th>Nota</th>
        </thead>
        <tbody>
          <tr v-for="(user, index) in usersToShow" :key="index" :class="getClass(user.nota)">
            <td>{{user.name}}</td>
            <td >{{user.nota}}</td>
          </tr>
          <tr v-if="usersToShow.length > 0" :class="getClass(promedio)">
            <td>Promedio:</td>
            <td>{{promedio}}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-components-table-users',
    props: ['usersToShow'],
    data () {
      return {
      }
    },
    mounted () {

    },

    methods: {
      reducer(accumulator, currentValue) {
        return accumulator + currentValue;
      },

      getClass(value) {
        let typ = '';

        if (value <= 4) {
          typ = [{'bg-danger': true}];
        }

        if (value > 4) {
          typ = [{'bg-warning': true}];
        }

        if (value > 7) {
          typ = [{'bg-success': true}];
        }

        return typ;
      },

    },
    computed: {
      promedio: (vm) => {
        let arrOfNotes = vm.usersToShow.map(us => {
          return us.nota;
        })

        return (arrOfNotes.reduce(vm.reducer)) / vm.usersToShow.length;
      },
    },
}


</script>


