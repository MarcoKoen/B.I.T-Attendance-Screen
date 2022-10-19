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
    background-color: beige;
    margin: auto;
    display: flex;
    flex-direction: column;
    text-align: center;
  }
  

</style>