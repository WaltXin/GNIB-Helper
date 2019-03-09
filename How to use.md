# GNIB
Usually, ticket released every day at 12 or 14:30(Time in Ireland).
#### Website
https://burghquayregistrationoffice.inis.gov.ie/Website/AMSREG/AMSRegWeb.nsf/AppSelect?OpenForm
#### 1. Input your information first
#### 2. Open Console
#### Windows:
In Chrome/FireFox: Press F12
![Imgur](https://i.imgur.com/Q8fc2Fk.png "GNIB console")
#### Mac:
![Imgur](http://wickedlysmart.com/wp-content/uploads/2014/03/ChromeConsole.jpg "GNIB console")

#### 3. Input code:Copy the following code to console
```js
// change to the date range you want  yyyy/mm/dd
var fromDate = new Date('2019/01/05');
var toDate = new Date('2019/02/25');
fromDate.setHours(0, 0, 0, 0);
toDate.setHours(0, 0, 0, 0);

var intervalId = null;
var weirdSound= new Audio("https://www.freesound.org/data/previews/256/256458_4772965-lq.mp3");
var monthNames = ["January", "February", "March", "April", "May", "June",
  "July", "August", "September", "October", "November", "December"
];

var slotWithDesiredDateFound = function (slotElements) {
	console.log('Performing date range check');
	for(let i=0; i<slotElements.length; i++) {
		var slotDate = getDateTimeFromGSlotString(slotElements[i].textContent);
		//slot date matches the range desired
		if(slotDate.getTime() >= fromDate.getTime() && slotDate.getTime() <= toDate.getTime()) {
			console.log('This is a match!');
			return true;
		} else {
			console.log('Not match, continue...');
		}
	}	
	return false;
}
//convert date string e.g. 13 November 2017 - 12:00 to date object
var getDateTimeFromGSlotString = function (dateString) {
	let valueArray = dateString.replace('Book This','').split(' ');
	let day = valueArray[0];
	let month = monthNames.indexOf(valueArray[1]) + 1;
	let year = valueArray[2];
	var newDateString  = year + '/' + month + '/' + day;
	console.log('The slot date is ' + newDateString);
	let formattedDate = new Date(newDateString);
	formattedDate.setHours(0, 0, 0, 0);
	return formattedDate;
}	
	
intervalId = setInterval(function () {
	let slotsAvailable= document.getElementsByClassName("appOption");
	if(slotsAvailable.length === 0) {	
		document.getElementById("btSrch4Apps").click();
		console.log("No slot found, job ran time:" + new Date());
	}	else if(!slotWithDesiredDateFound(slotsAvailable)){   //Comment out this else if block if you don't want to check the date range
		document.getElementById("btSrch4Apps").click();
		console.log("Slot found but date does not match what you want, job ran time: " + new Date());
	}	else {
		console.log("Slot found!!! Job ran time:" + new Date());
		//Play some weird sound :)
		weirdSound.play();
		alert("Slot found, hurry!!!");
		clearInterval(intervalId);
}}, 3000);
```
#### It should look like
![Imgur](https://i.imgur.com/RxLpBZk.png "input js")

### 4. Click return/enter bottom
![Imgur](https://i.imgur.com/ZWPmcuH.jpg "return")

### 5. Staring at the screen, once get notified, BOOK ASAP.

