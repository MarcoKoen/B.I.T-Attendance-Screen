<script>
  import {onMount} from 'svelte';

let studentsList = [];


onMount(async () => {
  const res = await fetch('https://randomuser.me/api/?results=20')
  const resResponse = await res.json()
  studentsList = resResponse.results;
  console.log(studentsList)
})

</script>

<form id="roles-form" action="#">
  <fieldset>
    <table>
      <thead>
        <tr>
          <th>Photo</th>
          <th>Surname</th>
          <th>First Name</th>
          <th>ID Number</th>
          <th>Attendance</th>
          <th>Today's Attendance</th>
        </tr>
      </thead>
      <tbody id="role-table-body">
        <!-- Comes from selected person's data -->
          {#each studentsList as student}
            <tr>
              <td><img src={student.picture.thumbnail} alt={student.name.first} style="width:50%;"></td> 
              <td>{student.name.last}</td> 
              <td>{student.name.first}</td>
              <td>{student.cell}</td>
            </tr>
          {/each}
      </tbody>
    </table>
    </fieldset>
</form>






<style>
 #roles-form{
   width: 80%;
   justify-content: center;
   margin: auto;
 }
 table {
  table-layout: fixed;
  width: 100%;
  border-collapse: collapse;
}
tr,td {
  padding-left: 4.5%;
  height: 20%;
}

thead{
  border-radius: 15px;
  border:15%;
  background-color: beige;
  outline-color:black;
  outline-style: groove;
}







</style>