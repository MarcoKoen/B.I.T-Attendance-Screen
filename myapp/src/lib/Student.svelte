<script>
  import {onMount} from 'svelte';
let nameObject = {name: '', lastName: '', photo:''}

let studentsList = [];

onMount(async () => {
  const res = await fetch('https://randomuser.me/api/?results=20')
  const resResponse = await res.json()
  studentsList = resResponse.results;
  console.log(studentsList)
})




</script>

<div class = "main-tab">
  <p>Paper Selected: Introductionary App Development</p>
  <ul class = "fields">
    <li>Photo</li>
    <li>Surname</li>
    <li>First Name</li>
    <li>ID Number</li>
    <li>Attendance</li>
    <li>Today's Attendance</li>
  </ul>

  <form id="student-form" action ="#">
    <fieldset>
      <tbody id="student-table-body" class ="studentData">
        {#each studentsList as student}
       <li><img src={student.picture.thumbnail} alt={student.name.first} style="width:auto;"></li> 
       <li>{student.name.last}</li> 
       <li>{student.name.first}</li>
        {/each}
      </tbody>
    </fieldset>
  </form>
</div>





<style>
.main-tab{
    border-radius: 15px;
    width: 90%;
    background-color: beige;
    margin: auto;
    display: flex;
    flex-direction: column;
  }

   .main-tab, .p {
    font-weight: 300;
  }

  .fields{
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    list-style-type: none;
  }

  .studentData{
    display: flex;
    flex-direction: row;
  }

</style>