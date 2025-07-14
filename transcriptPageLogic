// Initialization. Grabbing necessary elements.
let checkboxes = document.querySelectorAll('.cb');
let printViewCme = document.querySelectorAll('.print-view-cme');
let lineItem  = document.querySelectorAll('.transcript-line-item');
let printTranscriptBtn = document.getElementById("printTranscriptBtn");
let claimCmeBtn = document.getElementById("claimCmeBtn");
let totalCredits = document.getElementById("totalCredits");
let saveBtn = document.getElementById("dnn_ctr7776_Form_ctl00_btnSave");
let cmeCreditField = document.getElementById("dnn_ctr7776_Form_ctl00_uscFormTabEdit_pnlFields_i0_i2_rptCols_ctl00_txt");
let transcriptSavedYes = document.getElementById("dnn_ctr7776_Form_ctl00_uscFormTabEdit_pnlFields_i0_i2_rptCols_ctl01_rbl_0");
let textArea = document.querySelector('#dnn_ctr7776_Form_ctl00_uscFormTabEdit_pnlFields_i0_i3_rptCols_ctl00_txa').textContent;
let sessionCodes = document.querySelectorAll('td[data-cell="code"]');
let eduItem = document.querySelector('#dnn_ctr7776_Form_ctl00_uscFormTabEdit_pnlFields_i0_i1_rptCols_ctl00_uscLookup_acbLookup_taglist');
let saveAlert = document.querySelector('#save-alert');

saveBtn.classList.add('d-none', 'mt-0');

if (cmeCreditField.value != "0" && cmeCreditField.value.trim() != "") {
    claimCmeBtn.classList.remove('d-none');
}

if(textArea.trim() != "") {
    shouldICheckDaBox(sessionCodes,textArea);
}

document.querySelector('#dnn_ctr7776_Form_ctl00_uscFormTabEdit_pnlFields').classList.add('d-none');

for (let chkbox of checkboxes) {
    hideShowSession(chkbox);
}

let seshDateArr = [];
for(let chkbox of checkboxes) {
    if(chkbox.checked) {
        seshDateArr.push(chkbox.parentElement.parentElement.nextElementSibling.nextElementSibling.nextElementSibling.textContent);  
    }
}
console.log(seshDateArr)

let seshDateArrUnique = new Set(seshDateArr);
console.log(seshDateArrUnique)

// Error Handling to ensure progress is saved
for (let chkbox of checkboxes) {
    chkbox.onclick = (e) => {
        if(saveAlert.classList.contains('d-none')) {
            saveAlert.classList.remove('d-none');
        }

        if(saveBtn.classList.contains('d-none')) {
            saveBtn.classList.remove('d-none');
        }

        if(!printTranscriptBtn.classList.contains('disabled')) {
            printTranscriptBtn.classList.add('disabled');
        }

        if(!claimCmeBtn.classList.contains('disabled')) {
            claimCmeBtn.classList.add('disabled');
        }
    }
}



// Calculation of credits
function calculateViewCme(cbs) {
    let creditObject = {score: 0};

    for (let checkbox of cbs) {
        if (checkbox.checked) {
            let cme = checkbox.parentElement.parentElement.parentElement.lastElementChild.textContent;
            let cmeAmount = Number.parseFloat(cme);
            creditObject.score += cmeAmount;
        }
    }
    return creditObject.score;
}

// Deprecated function. Might be useful later...
function calculatePrintCme(credits) {
    let creditObject = {score: 0};

    for (let credit of credits) {
        let cond = credit.parentElement.classList.contains('d-none');
        if(!cond){
            let cmeValueText = credit.textContent;
            let cmeValue = Number.parseFloat(cmeValueText);
            creditObject.score += cmeValue;
        }
    }
    return creditObject.score;
}

// hide-show logic for initialization and checkboxes
function hideShowSession (cb) {
	let session    =  cb.parentElement.parentElement.nextElementSibling.nextElementSibling.textContent;
	let inputField 	=  document.querySelector('#dnn_ctr7776_Form_ctl00_uscFormTabEdit_pnlFields_i0_i3_rptCols_ctl00_txa');

	let currentText = inputField.textContent;

	if (cb.checked) {
        alreadyExist(currentText, session, inputField);
        showLineItem(lineItem,session);
        cmeCreditField.value = calculateViewCme(checkboxes);
	} else {
        inputField.textContent = cleanString(currentText, session);
        hideLineItem(lineItem,session);
        cmeCreditField.value = calculateViewCme(checkboxes);
	}
}

function cleanString(text, sesh) {
	let cleansedString = text.split(`${sesh},`).join('');
	return cleansedString;
}

function alreadyExist(text, sesh, field) {
	let condition = text.includes(`${sesh},`);

	if(!condition) {
		return field.innerText = text + sesh + ",";
	}
}


function showLineItem (rows, code) {

    for (let row of rows) {
        let cond = row.id;
        if (code === cond) {
            row.classList.remove('d-print-none') 
        }
    }
}

function hideLineItem (rows, code) {

    for (let row of rows) {
        let cond = row.id;
        if (code === cond) {
            row.classList.add('d-print-none') 
        }
    }
}

// Deciding what should be checked when the page loads
function shouldICheckDaBox (codes,txt) {
    
    for (let code of codes) {
        let sessioncode = code.textContent;
        if (txt.includes(`${sessioncode},`)) {
            code.previousElementSibling.previousElementSibling.firstElementChild.firstElementChild.checked = true;
        }
    }
}

// Print button logic
printTranscriptBtn.onclick = (e) => {
    e.preventDefault();
    if((seshDateArrUnique.size !== seshDateArr.length) && !itemCode.includes("OD")) {
        claimCmeBtn.classList.add('disabled');
        printTranscriptBtn.classList.add('disabled');
        alert("You can only select one concurrent session.");
    } else {
        totalCredits.textContent = calculateViewCme(checkboxes);
        window.print();   
    } 
}

// CME button logic
claimCmeBtn.onclick = (e) => {
    e.preventDefault();
    if((seshDateArrUnique.size !== seshDateArr.length) && !itemCode.includes("OD")) {
        claimCmeBtn.classList.add('disabled');
        printTranscriptBtn.classList.add('disabled');
        alert("You can only select one concurrent session.");
    } else {
        window.location.href = `https://www.spine.org/Education/CME-Certificate?EID=${itemCode}`;    
    }    
}