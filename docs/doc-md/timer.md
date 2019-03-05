## Device.StartTimer
```cs
Device.StartTimer(TimeSpan.FromSeconds(30), () =>
{
    // Do something
   
    return true; // True = Repeat again, False = Stop the timer
});
```

## Navigating to next page after specified time
```cs
CountDown = CountDownLimit;

Device.StartTimer(TimeSpan.FromSeconds(1), () => {
	
	CountDown -= 1;
	
	Device.

	if(CountDown >= 1){
		Navigation.PushAsync(new ResultPage());
	}
	
	return CountDown >= 1;
});
```
