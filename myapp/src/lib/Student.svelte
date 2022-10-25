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
    <table>
        <tr>
          <th>Photo</th>
          <th>Surname</th>
          <th>First Name</th>
          <th>ID Number</th>
          <th>Attendance</th>
          <th>Today's Attendance</th>
        </tr>
      <tbody id="role-table-body">
          {#each studentsList as student}
            <tr>
              <td><img src={student.picture.thumbnail} alt={student.name.first} style="width:50%;"></td> 
              <td>{student.name.last}</td> 
              <td>{student.name.first}</td>
              <td>{student.cell}</td>
              <td class= "attendance-value">
                <div class="square green">P</div>
                <div class="square red">A</div>
                <div class="square green">P</div>
                <div class="square green">O</div>
                <div class="square red">A</div>
              </td>
            </tr>
          {/each}
      </tbody>
    </table>

</form>


<style>
 #roles-form{
   width: 80%;
 }
 table {
  table-layout: fixed;
  width: 100%;
}

.attendance-value{
  display: flex;
  padding-top: 25px;
  gap:1%;

}

.square{
  height:2rem;
  width:2rem;
  font-weight: bold;
  border-style: solid;
  border-color: black;
  color:white;

}

.green{
  background-color: green;
}

.red{
  background-color: red;
}

</style>