<script>
  import { onMount } from 'svelte'

  export let data;
  let current = new Date()
  onMount(() => {
    setTimeout(function(){current = new Date();}, 60000);
	})
  
  $: calculateDate = (date) => {
    date = new Date(date);
      
    // To calculate the time difference of two dates
    let diff = current.getTime() - date.getTime();
      
    // Calculate difference between the date and now
    let diffDay = (diff / (1000 * 3600 * 24))
    let diffHour = (Math.abs(diff) / 36e5)
    let diffMin = (Math.round((diff/1000)/60))
    console.log(diffDay, diffHour, diffMin)
    
    //return the correct string
    if(diffDay >= 1 && diffDay < 2){
      return Math.round(diffDay) + " day ago"
    }else if(diffDay > 1){
      return Math.round(diffDay) + " days ago"
    }
    if(diffHour >= 1 && diffHour < 2){
      return Math.round(diffDay) + " hour ago"
    }else if(diffHour > 1){
      return Math.round(diffHour) + " hours ago"
    }
    if(diffMin >= 1 && diffMin < 2){
      return Math.round(diffMin) + " minute ago"
    }else if(diffMin > 1){
      return Math.round(diffMin) + " minutes ago"
    }
    return "just now" 
  }
</script>

<style>
  *{
    margin: 0;
  }

  main {
    margin-bottom: 35px;
  }

  h1{
    display: flex;
    flex-direction: column;
    font-size: 14px;
  }
  h2{
    font-size: 14px;
    color: var(--secondary);
    font-weight: 400;
    margin-bottom: 10px;
  }
  p {
    font-size: 15px;
  }
</style>

<main>
  <h1>{data.user}</h1>
  <h2>{calculateDate(data.date)}</h2>
  <p>{data.content}</p>
</main>