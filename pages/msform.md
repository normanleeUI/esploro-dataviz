---
title: microsoft form
layout: about
permalink: /msform.html
---

<!-- TODO
Finish form
finish apicall function (find out how to get value from radio buttons)
fix the CORS access for API calls
fix the invalid URL for api calls
change the //construct URL section to refer to variables, rather than static strings
Add validation to pub year form
begin fleshing out displayData function
choose visualization method and/or html enhancement methods, re-evaluate use-cases
 -->

//report filters form
<form id="apiParams" onsubmit="apiCall()">

<label for="affiliation" class="form-label">affiliations</label>
<input type="text" id="affiliation" class="form-control" aria-describedby="affiliationHelp">
<div id="affiliationHelp" class="form-text mb-4">
    <strong>Not required</strong>. Enter any UI affiliations you would like to use as a filter.
    </div>

<label for="pubYearString" class="form-label">Publication Year</label>
<input type="text" id="pubYearString" class="form-control" aria-describedby="pubYearHelp">
<div id="pubYearHelp" class="form-text mb-4">
    <strong>Not required</strong>. Required format: YYYY.
    </div>

<label for="pubBefore" class="form-label">All assets published before this year (inclusive)</label>
<input type="radio" id="pubBefore" class="form-control" name="pubYearBool" value="pubBefore">
<label for="pubAfter" class="form-label">All assets published after this year (inclusive)</label>
<input type="radio" id="pubAfter" class="form-control" name="pubYearBool" value="pubAfter">

<label for="doi" class="form-label">Only retrieve assets with a DOI</label>
<input type="radio" id="doi" class="form-control" name="doiBool" aria-describedby="doiHelp" value="doi">

<label for="citations" class="form-label">Only retrieve assets with one or more citations</label>
<input type="radio" id="citations" class="form-control" name="citationBool" aria-describedby="doiHelp" value="citations">
   
<button type="submit" class="btn btn-primary">Submit API Call</button>

</form>

<!-- Bootstrap JS bundle -->
<script src="/qr-generator/assets/lib/bootstrap.bundle.min.js"></script>
<!-- load other optional js -->
<script src="/qr-generator/assets/lib/qr-code-styling.js"></script>

<script> 
// do something with the json function
function displayData(json) {
    var contentDiv = document.getElementById('example');
    // iterate over the json object
    contentDiv.innerHTML = '<h2>Example</h2>';

}

// fetch the json
async function getData() {
	try {
		const response = await fetch(url.toString());
		if (!response.ok) {
			throw new Error(`Response status: ${response.status}`);
		}
        // parse the json response
		const json = await response.json();
        // do something with the json
        console.log(json);
		
	} catch (error) {
		console.error(error.message);
	}
}

getData();

function apiCall() {
//get values
var affiliation = document.getElementById("affiliation").value;
var pubYear = document.getElementById("pubYearString").value;
var pubYearBool = document.getElementByName("pubYearBool")

// construct the url 
var baseUrl = "https://api-na.hosted.exlibrisgroup.com/esploro/v1/researchanalytics/reports";
const url = new URL(baseUrl);
url.search = new URLSearchParams({
	apikey: 'l8xx3ed522f0c1f24078bdb30013d5bdf505',
	format: 'json',
	path: 'shared/University of Idaho/Reports/normTesting/forViz',
	limit: 1000

});
//make call
}

apiCall();