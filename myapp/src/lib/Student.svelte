<script>
  import {onMount} from 'svelte';
  import { debug, text } from 'svelte/internal';
  

let studentsList = [];
let presentCount, absentCount, otherCount, onlineCount;

let attendanceOptions = [
    { text:'Select Attendance'},
		{ value: 'present', text: 'Present' },
		{ value: 'absent', text: 'Absent' },
		{ value: 'online', text: 'Online' },
		{ value: 'other', text: 'Other' },
	];

onMount(async () => {
  const res = await fetch('https://randomuser.me/api/?results=20')
  const resResponse = await res.json()
  studentsList = resResponse.results;
  console.log(studentsList)
})

let attendances = {};
	$: attendancesValues = Object.values(attendances);
	$: presentCount = attendancesValues.filter(s => s == 'present').length;
	$: absentCount = attendancesValues.filter(s => s == 'absent').length;
	$: onlineCount = attendancesValues.filter(s => s == 'online').length;
	$: otherCount = attendancesValues.filter(s => s == 'other').length;



</script>

<form id="roles-form" action="#">
  <div class="student-count">
  <p>Present:{presentCount}</p>
  <p>Absent:{absentCount}</p>
  <p>Other:{otherCount}</p>
  <p>Online:{onlineCount}</p>
</div>
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
                  <select bind:value={attendances[student.name.first]}>
                    {#each attendanceOptions as answers}
                      <option value={answers.value}>
                        {answers.text}
                      </option>
                    {/each}
                  </select>        
                  <button>&#10003;</button>
                  <button>&#10540;</button>
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

.student-count{
  display: flex;
}

.student-count , p{
  padding-left: 2rem;
}


</style>