# WD101

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="style.css" />
    <title>Task</title>
  </head>
  <body>
    <header style="text-align: center">Welcome To My Site</header>
    <h1>Fill the Form</h1>
    <div class="main">
      <div class="form">
        <h4 style="text-align: center">Register Form</h4>
        <form id="user-form">
          <label for="name">Name : </label>
          <input required type="text" name="name" id="name" />
          <br />
          <label for="email">Email : </label>
          <input required type="email" name="email" id="email" />
          <br />
          <label for="password">Password : </label>
          <input required type="password" name="password" id="password" /><br />
          <label for="dob">DOB : </label>
          <input type="date" name="dob" id="dob" required />
          <br />
          <input
            style="width: 40px"
            type="checkbox"
            name="acceptTerms"
            id="acceptTerms"
          />
          <label for="acceptTerms">Accept terms & Conditions</label>
          <br /><br />
          <input
            style="background-color: rgb(19, 151, 19); color: white"
            type="submit"
            value="Submit"
          />
        </form>
      </div>
    </div>
    <div id="entrytbale"></div>
    <script src="./scriptjs.js"></script>
  </body>
</html>
Skip to content
Search or jump to…
Pulls
Issues
Marketplace
Explore
 
@pranaylenkathi 
pranaylenkathi
/
function validateAge(today, dobobj) {
  var age = today.getFullYear() - dobobj.getFullYear();
  var m = today.getMonth() - dobobj.getMonth();
  if (m < 0 || (m === 0 && today.getDate() < dobobj.getDate())) {
    age--;
  }
  return age;
}
let dobelement = document.getElementById("dob");
dobelement.addEventListener("change", () => {
  let [y,m,d] = document.getElementById("dob").value.split("-");
  let dob = new Date(y,m,d);
  let Today = new Date();
  age = validateAge(Today, dob);
  if (age < 18 || age > 55) {
    dobelement.setCustomValidity("age must lie in 18 and 55 years!!!");
 
    return;
  } else {
    dobelement.setCustomValidity("");
  }
});
let form = document.getElementById("user-form");

const retriveEntries = () => {
  let entries = localStorage.getItem("userEntry");

  if (entries) {
    entries = JSON.parse(entries);
  } else {
    entries = [];
  }
  return entries;
};

let Entries = retriveEntries();

const displayEntries = () => {
  const entries = retriveEntries();

  const rows = entries
    .map((entry) => {
      const name = `<td class="td">${entry.name}</td>`;
      const email = `<td class="td">${entry.email}</td>`;
      const password = `<td class="td">${entry.password}</td>`;
      const dob = `<td class="td">${entry.dob}</td>`;
      const acceptTerms = `<td class="td">${entry.acceptTerms}</td>`;

      const row = `<tr>${name} ${email} ${password} ${dob} ${acceptTerms}</tr>`;
      return row;
    })
    .join("\n");

  let tableDiv = document.getElementById("entrytbale");

  tableDiv.innerHTML = `<table>
  <tr>
    <th class="th">Name</th>
    <th class="th">Email</th>
    <th class="th">Password</th>
    <th class="th">Dob</th>
    <th class="th">Accepted terms?</th>
  </tr>
    ${rows}
  </table>`;
};

// const saveUserFrom = () => {
const saveUserFrom = (event) => {
  event.preventDefault();

  let name = document.getElementById("name").value;
  let email = document.getElementById("email").value;
  let password = document.getElementById("password").value;
  let dob = document.getElementById("dob").value;
  let acceptTerms = document.getElementById("acceptTerms").checked;

  let entry_obj = {
    name,
    email,
    password,
    dob,
    acceptTerms,
  };

  Entries.push(entry_obj);

  localStorage.setItem("userEntry", JSON.stringify(Entries));

  displayEntries();
};

form.addEventListener("submit", saveUserFrom);

displayEntries();
const email = document.getElementById("email");
email.addEventListener("input", () => validate(email));
function validate(ele) {
  if (ele.validity.typeMismatch) {
    ele.setCustomValidity("The Email is not in the right format!!!");
    ele.reportValidity();
  } else {
    ele.setCustomValidity("");
  }
}
body{
    background-color: rgb(231, 240, 212);
}
header{
    background-color: rgb(166, 231, 15);
    padding: 30px;
    font-size: 25px;
    font-family:Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
}
.main{
  
padding: 20px;
    font-family: Arial, Helvetica, sans-serif;
}
.form{
    padding: 40px;
    background-color: gray;
    box-sizing: border-box;
    border: 2px solid rgb(93, 11, 11) ;
    box-shadow: 100px;
    text-align: center;

}
.form h4{
   font-size: 30px;
}
.form label{ 
   font-size: 15px;
   font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
   font-weight: 600;

   
   
}
.form input{
    background-color: transparent;
   font-size: 15px;
   width: 50%;
border: none;
   border-bottom: solid;
   height: 30px;
   border-radius: 5px;
   
   
}
table{
    text-align: center;
    border: solid 4px;
}
td{
    border:solid 2px;
}
th{
    border:solid 2px;
}
