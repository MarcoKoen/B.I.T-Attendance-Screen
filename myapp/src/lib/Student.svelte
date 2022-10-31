<script>
  import {onMount} from 'svelte';
  import { debug } from 'svelte/internal';
  

let studentsList = [];

onMount(async () => {
  const res = await fetch('https://randomuser.me/api/?results=20')
  const resResponse = await res.json()
  studentsList = resResponse.results;
  console.log(studentsList)
})

</script>

<form id="roles-form" action="#">
  <p>Present: Absent: Other: Online: </p>
  <table>
        <tr>
          <th>Photo</th>
          <th>Surname</th>
          <th>First Name</th>
          <th>Attendance</th>
          <th>Today's Attendance</th>
        </tr>
      <tbody id="role-table-body">
          {#each studentsList as student}
            <tr>
              <td><img src={student.picture.thumbnail} alt={student.name.first} style="width:50%;"></td> 
              <td>{student.name.last}</td> 
              <td>{student.name.first}</td>
              <td class= "attendance-value">
                <div class="square green" title= "Monday 15th of October">P</div>
                <div class="square red" title= "Wednesday 19th of October">A</div>
                <div class="square green" title= "Monday 25th of October">P</div>
                <div class="square green" title= "Wednesday 30th of October">O</div>
                <div class="square red" title= "Monday 5th of November">A</div>
              </td>
              <td>
                <div class="custom-select">
                  <select>
                    <option value="0">Select Status:</option>
                    <option value="1">Present</option>
                    <option value="2">Online Present</option>
                    <option value="3">Absent</option>
                    <option value="4">Sick</option>
                    <option value="5">Late</option>
                  </select>
                  <span>&#10003;</span>
                  <span>&#10540;</span>
                </div>
              </td>
            </tr>
          {/each}
      </tbody>
    </table>

</form>


<style>
 #roles-form{
   width: 80%;
   font-size:x-large;
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

.square:hover{
  filter:brightness(70%);
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