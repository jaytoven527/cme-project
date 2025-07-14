let alreadySubmitted = '<%# Eval("nass_surveysubmitted")%>';
let linkProvided  = '<%# Eval("ac-nass_surveyurl")%>';
let msForm = '<%# Eval("ac-nass_msformsid")%>';
let idQuestion = '<%# Eval("ac-nass_idquestion")%>';
let contactNumber = '<%# Eval("a_f2f92ab8a09beb11b1ac000d3a540e79-pa_contactnumber")%>';
let surveyClosed  = new Date('<%# Eval("ac-nass_surveyclose")%>');
let surveyOpen    = new Date('<%# Eval("ac-nass_surveyopen")%>');
let surveyOpenText = '<%# Eval("ac-nass_surveyopen")%>';
let surveyClosedText = '<%# Eval("ac-nass_surveyclose")%>';
const currentDate = new Date();
const notAvailable = document.querySelector("#NotAvailable");
let educationActivity = '<%# Eval("pa_educationactivityid")%>';
let transcript = '<%# Eval("ac-nass_transcript")%>';
let cmeCredit = '<%# Eval("nass_cmecredit")%>';

const parseEducationActivity = (edu) => {
  let omitFirstChar = edu.replace("{", "");
  let omitLastChar  = omitFirstChar.replace("}", "");

  return omitLastChar;
}

educationActivity = parseEducationActivity(educationActivity);

console.log(educationActivity)

notAvailable.classList.add("d-none");

console.log(alreadySubmitted.trim() != "")
console.log(alreadySubmitted)
console.log(linkProvided.trim() == "")
console.log(surveyClosed < currentDate)
console.log('<%# Eval("pa_customerid")%>')

if ((surveyOpenText.trim() == "" && surveyClosedText.trim() == "") || alreadySubmitted.trim() != "" || surveyClosed < currentDate) {
    transcript === "Yes" && (cmeCredit == "0" || cmeCredit.trim() == "") ? window.location.href = `https://www.spine.org/Education/Transcript?m=${meetingId}&edu=${educationActivity}` : cmeCheck();
} else {
  cmeCheck();
}



function surveyCheck () {
  if (linkProvided.trim() != "") {
    window.location.href = linkProvided;
  } else if (msForm.trim() != "" && idQuestion.trim() != "") {
    window.location.href = `https://forms.office.com/Pages/ResponsePage.aspx?id=${msForm}&${idQuestion}=${educationActivity}`;
  } else {
    window.print();
    console.log("Certificate should be printing. If not, please check MX Template.<br/>MX Template: NASS-CMESurveyRedirect")
  }
}

function cmeCheck () {
  if (alreadySubmitted.trim() != "" || surveyClosed < currentDate) {
  console.log("Certificate should be printing. If not, please check MX Template.<br/>MX Template: NASS-CMESurveyRedirect")
} else if (surveyOpen > currentDate || surveyOpenText.trim() == "") {
  console.log("Survey is not open yet");
  notAvailable.classList.remove("d-none");
} else if (surveyOpen <= currentDate) {
  surveyCheck();
}
}