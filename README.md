# TOP-ENG
هو فريق مختص في كلية الهندسة المدنية 
<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>موقع الفريق</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>

<style>
body { font-family: Arial; direction: rtl; margin: 0; background:#f4f4f4; }
header { background:#222; color:white; padding:20px; text-align:center; }
.logo { font-size:30px; font-weight:bold; }
.container { padding:20px; }

button {
  padding:10px 15px;
  margin:10px;
  cursor:pointer;
}

.card {
  background:white;
  padding:15px;
  margin-top:15px;
  border-radius:10px;
}

#formBox { display:none; background:white; padding:15px; border-radius:10px; }

select, input { width:100%; padding:8px; margin:5px 0; }

.hidden { display:none; }
</style>
</head>

<body>

<header>
  <div class="logo">لوغو الفريق</div>
  <p>موقع الفريق التجاري</p>
</header>

<div class="container">

<div class="card">
  <h3>من نحن؟</h3>
  <p>تعريف عن الفريق: نحن فريق طلابي يهدف لتنظيم التسجيل والمتابعة الأكاديمية.</p>
</div>

<button onclick="openContact()">تواصل معنا</button>
<button onclick="toggleForm()">اشتراك</button>
<button onclick="downloadExcel()">تحميل البيانات Excel</button>

<!-- CONTACT -->
<div id="contactBox" class="card hidden">
  <h3>تواصل معنا</h3>
  <p>واتس: 000000000</p>
  <p>تلجرام: @team</p>
  <p>انستا: @team</p>
</div>

<!-- FORM -->
<div id="formBox">
  <h3>نموذج الاشتراك</h3>

  <input id="name" placeholder="اسم الطالب">
  <input id="number" placeholder="رقم الطالب">
  <input id="card" placeholder="رقم البطاقة">
  <input id="invoice" placeholder="رقم الفاتورة">

  <label>السنة الدراسية</label>
  <select id="year" onchange="updateSubjects()">
    <option value="">اختر</option>
    <option value="1">سنة أولى</option>
    <option value="2">سنة ثانية</option>
  </select>

  <div id="year1" class="hidden">
    <label>ميكانيك هندسي 1</label>
    <select id="mech1">
      <option>بارزي</option>
      <option>صقر</option>
      <option>جبل</option>
    </select>

    <label>رياضيات 1</label>
    <select id="math1">
      <option>أبو ضاهر</option>
      <option>كلية</option>
      <option>مصري</option>
    </select>
  </div>

  <div id="year2" class="hidden">
    <label>الموائع</label>
    <select id="fluid">
      <option>ابراهيم</option>
      <option>اسكندر</option>
      <option>علي</option>
      <option>حبال</option>
    </select>

    <label>مقاومة 1</label>
    <select id="resist">
      <option>رهف</option>
      <option>حمصي</option>
      <option>سودان</option>
    </select>

    <label>رياضيات 3</label>
    <select id="math3">
      <option>سكري</option>
      <option>دنان</option>
      <option>خطيب</option>
    </select>
  </div>

  <button onclick="saveData()">حفظ</button>
</div>

</div>

<script>

let data = [];

function openContact(){
  document.getElementById("contactBox").classList.toggle("hidden");
}

function toggleForm(){
  let f = document.getElementById("formBox");
  f.style.display = (f.style.display === "block") ? "none" : "block";
}

function updateSubjects(){
  let year = document.getElementById("year").value;
  document.getElementById("year1").classList.add("hidden");
  document.getElementById("year2").classList.add("hidden");

  if(year === "1") document.getElementById("year1").classList.remove("hidden");
  if(year === "2") document.getElementById("year2").classList.remove("hidden");
}

function saveData(){
  let entry = {
    اسم: document.getElementById("name").value,
    رقم: document.getElementById("number").value,
    بطاقة: document.getElementById("card").value,
    فاتورة: document.getElementById("invoice").value,
    سنة: document.getElementById("year").value
  };

  if(entry.سنة === "1"){
    entry.ميكانيك = document.getElementById("mech1").value;
    entry.رياضيات1 = document.getElementById("math1").value;
  }

  if(entry.سنة === "2"){
    entry.موائع = document.getElementById("fluid").value;
    entry.مقاومة = document.getElementById("resist").value;
    entry.رياضيات3 = document.getElementById("math3").value;
  }

  data.push(entry);
  alert("تم الحفظ!");
}

function downloadExcel(){
  let ws = XLSX.utils.json_to_sheet(data);
  let wb = XLSX.utils.book_new();
  XLSX.utils.book_append_sheet(wb, ws, "Students");
  XLSX.writeFile(wb, "students.xlsx");
}

</script>

</body>
</html>
