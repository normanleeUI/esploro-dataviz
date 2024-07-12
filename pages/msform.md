---
title: microsoft form
layout: about
permalink: /msform.html
---

<!-- TODO
Finish form
fix the CORS access for API calls
finish apicall function
fix the invalid URL for api calls
change the //construct URL section to refer to variables, rather than static strings
begin fleshing out displayData function
choose visualization method and/or html enhancement methods, re-evaluate use-cases
 -->

 <!-- Notes
 If you have the asset ID you can construct a URL to the asset's verso page.
 Possible use-case: export data then generate list of citations. (https://citationstyles.org/developers/)???
 -->

<!-- DONE
Add validation to pub year form
 -->

<!-- report filters form -->
<form id="apiParams" onsubmit="apiCall()">

<label for="keyword" class="form-label">Keywords</label>
<input type="text" id="keyword" class="form-control" aria-describedby="keywordHelp">
<div id="keywordHelp" class="form-text mb-4">
    <p>Enter any UI keywords you would like to use as a filter. Keyword searches: asset title and authors.</p>
    </div>

<label for="pubYearString" class="form-label">Publication Year</label>
<input type="date" step="365" id="pubYearString" class="form-control">

<label for="pubYearBool" class="form-label">All assets published (before or after) this year (inclusive)</label>
<select id="pubYearBool" class="form-control">
  <option value="pubYearBefore">Before</option>
  <option value="pubYearAfter">After</option>

<label for="doi" class="form-label">Only retrieve assets with a DOI</label>
<input type="radio" id="doi" class="form-control" name="doiBool" value="doi">

<label for="citations" class="form-label">Only retrieve assets with one or more citations</label>
<input type="radio" id="citations" class="form-control" name="citationBool" value="citations">

<!-- Making this a dropdown that includes checkboxes is a little tricky. See: https://www.geeksforgeeks.org/how-to-use-checkbox-inside-select-option-using-javascript/  -->
<!-- Can use "optgroup" for subunits: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select  -->
<label for="affiliation">Only retrieve assets from the following units</label>
<select id="affiliation" name="affiliation" size="14" multiple aria-describedby="affiliationHelp">
  <option value="n13085">College of Agricultural and Life Sciences</option>
  <option value="n31646">College of Art and Architecture</option>
  <option value="n9513">College of Business and Economics</option>
  <option value="n5857">College of Education, Health, and Human Sciences</option>
  <option value="n19263">College of Engineering</option>
  <option value="n117014">College of Graduate Studies</option>
  <option value="n13969">College of Law</option>
  <option value="n14472">College of Letters, Arts, and Social Sciences</option>
  <option value="n259891">College of Natural Resources</option>
  <option value="n13549">College of Science</option>
  <option value="248278">James A. and Louise McClure Center for Public Policy Research</option>
  <option value="n8707">Office of Research and Economic Development</option>
  <option value="n91926">Office of the Provost and Executive Vice President</option>
  <option value="n6370">University of Idaho Library</option>
  <option value="n38176">WWAMI Medical Education Program</option>
</select>
<div id="affiliationHelp" class="form-text mb-4">
    <p>Note: selecting a College will return all assets from all units within that college. If no selection is made, returns assets from all units. Assets may be marked as belonging to multiple units, depending on authorship.</p>
    </div>
   
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
var keyword = document.getElementById("keyword").value;
var pubYear = document.getElementById("pubYearString").value;
var pubYearBool = document.getElementById("pubYearBool").value;
var doi = document.getElementById("doi").value;
var citations = document.getElementById("citations").value;
// This will be an associative array. Loop through it to parse: https://www.w3schools.com/php/php_arrays_associative.asp
var affiliation = document.getElementById("affiliation").value;

// construct the url
//report filters are not syntaxed like normal params. https://developers.exlibrisgroup.com/blog/Working-with-Analytics-REST-APIs/. Will need to see how the API console field 'filter' encodes them (but won't be able to do that until I can actually call the report and therefore check if the encoding returns an error message.)
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