<script>
 let currentDate = new Date().toJSON().slice(0, 10);
 let currentTime = new Date().toLocaleTimeString();

</script>

<div class = "header">
<h1>Daily Attendance Dashboard</h1>
<p>{currentDate} | {currentTime}</p>
</div>

<div class= "attendance-containter">

</div>



<style>
  .header{
    border-radius: 15px;
    height: 8rem;
    width: 90%;
    margin: auto;
    display: flex;
    flex-direction: column;
    text-align: center;
    outline-color:black;
    outline-style: groove;
  }
  

</style>