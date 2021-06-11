<template lang="html">

  <section class="src-components-table-answers">
    <div class="jumbotron">
      <table class="table">
        <thead>
          <th>Pregunta</th>
          <th>Respuesta</th>
        </thead>
        <tbody>
          <tr v-for="(question, index) in answers" :key="index">
            <td>{{question.num}}</td>
            <td >{{convertArrayToText(question.answer)}}</td>
          </tr>
        </tbody>
      </table>
    </div>


  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-components-table-answers',
    props: [],
    mounted () {

    },
    data () {
      return {
        answers: [
          {
            num: 1,
            answer: ['c']
          },
          {
            num: 2,
            answer: ['b', 'c']
          },
          {
            num: 3,
            answer: ['b', 'd']
          }

        ]
      }
    },
    methods: {
      convertArrayToText(arr) {
        return arr.join(' ');
      }
    },
    computed: {

    }
}


</script>

