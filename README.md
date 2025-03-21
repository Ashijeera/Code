Code GS
//code.gs

function doGet() {  
return HtmlService.createTemplateFromFile('index').evaluate()
      .setTitle("ระบบแจ้งผลการเรียน")
      .addMetaTag('viewport','width=device-width , initial-scale=1')
      .setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL)
} 

function search(obj) {
  var ss = SpreadsheetApp.getActive().getSheetByName('Data') 
  var data =  ss.getDataRange().getDisplayValues()
  var output = [];
  
  data.forEach(function(f) {
    if (~[f[0].toString().toLowerCase()].indexOf(obj.idcard)){
      output.push(f);
    }
  });
  return output;
}

HTML Code
<!doctype html>
<html lang="en">

<head>
  <base target="_top">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" />
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet">
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Thai&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Noto Sans Thai', sans-serif;
    }

    a {
      //color: #000;
      text-decoration: none;
    }
  </style>

</head>

<body>
  <div class="container">
    <div class="row">
      <div class="col-md-6 mx-auto">
        <div class="card text-center">
          <div class="card bg-white">
            <h5 class="card-header text-white bg-success"><i class="fas fa-search"></i> ผลการเรียนออนไลน์
            </h5>
            <form id="searchform" onsubmit="searchData(this)">
              <div class="card-body">
                <input class="form-control" type="text" name="idcard" style="text-align: center;"placeholder="พิมพ์หมายเลขบัตรประชาชน" maxlength="13" required>
              </div>
          </div>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col-md-6 mx-auto mt-2">
        <button type="submit" class ="btn btn-success text-white w-100" id="search-btn"> ค้นหา</button>
        <button class="btn btn-success w-100" type="button" disabled id="btn2" style="display:none">
 <span class="spinner-border spinner-border-sm" role="status" aria-hidden="true"></span>
  กำลังค้นหา...
</button>
        </form>
        <div class="mt-3" id="tb"> </div>

      </div>
    </div>

    <div class="container text-center">
     <div class="copyright mb-3"></div>
    </div>
  </div>
  <script>
    $(document).ready(()=>{
      setFooter()
     });

    function searchData(obj) {
      event.preventDefault()
      $('#search-btn').hide()
      $('#btn2').show() 
      google.script.run.withSuccessHandler(successData).search(obj);
    }

    function successData(data) {
       if(data && data !== undefined && data.length != 0){
      Swal.fire({
        position: 'top',
        icon: 'success',
        title: 'ยินดีด้วย..พบข้อมูลของคุณ',
        showConfirmButton: false,
        timer: 1500,
      })
 document.getElementById("tb").innerHTML = 
 `<table class="table table-bordered">  
        <thead class="p-3 mb-2 bg-success text-white">
        <tr>
        <th scope="col" colspan="12"><center><i class="fas fa-user-graduate"></i> ผลการเรียน</center></th>
        </tr>
        </thead>
        <tbody>
        <tr>
        <td colspan="12">${data[0][1]}</td>
        </tr> 
        <tr>
        <td colspan="12">${data[0][2]}</td>
        </tr> 
        <thead class="p-3 mb-2 bg-success text-white">
        <tr>
        <th scope="col" ><center>วิชา</center></th>
        <th scope="col"><center>คะแนน</center></th>
        <th scope="col"><center>เกรด</center></th>
        </tr>
        </thead>
        <tr>
        <td><b>${data[0][3]}</b></td>      
        <td ><center>${data[0][4]}</center></td>
        <td><b><center>${data[0][5]}</center></b></td>  
        </tr> 
        <tr>
        <td><b>${data[0][6]}</b></td>      
        <td ><center>${data[0][7]}</center></td>
        <td><b><center>${data[0][8]}</center></b></td>  
        </tr> 
        <tr>
        <td><b>${data[0][9]}</b></td>      
        <td ><center>${data[0][10]}</center></td>
        <td><b><center>${data[0][11]}</center></b></td>  
        </tr>
        <tr>
        <td><b>${data[0][12]}</b></td>      
        <td ><center>${data[0][13]}</center></td>
        <td><b><center>${data[0][14]}</center></b></td>  
        </tr>
        <tr>
        <td><b>${data[0][15]}</b></td>      
        <td ><center>${data[0][16]}</center></td>
        <td><b><center>${data[0][17]}</center></b></td>  
        </tr>
        <tr>
        <td><b>${data[0][18]}</b></td>      
        <td ><center>${data[0][19]}</center></td>
        <td><b><center>${data[0][20]}</center></b></td>  
        </tr>
        <tr>
        <td><b>${data[0][21]}</b></td>      
        <td ><center>${data[0][22]}</center></td>
        <td><b><center>${data[0][23]}</center></b></td>  
        </tr>
        <tr>
        <td><b>${data[0][24]}</b></td>      
        <td ><center>${data[0][25]}</center></td>
        <td><b><center>${data[0][26]}</center></b></td>  
        </tr>
        <tr>
        <td><b>${data[0][27]}</b></td>      
        <td ><center>${data[0][28]}</center></td>
        <td><b><center>${data[0][29]}</center></b></td>  
        </tr>
        <tr>
        <td><b>${data[0][30]}</b></td>      
        <td ><center>${data[0][31]}</center></td>
        <td><b><center>${data[0][32]}</center></b></td>  
        </tr>
        <tr>
        <td><b>${data[0][33]}</b></td>      
        <td ><center>${data[0][34]}</center></td>
        <td><b><center>${data[0][35]}</center></b></td>  
        </tr>
      
        <tr>
        <td><b>เกรดเฉลี่ย</b></td>      
        <td colspan="10" style="color:red;font-size:15px;"><b><center>${data[0][36]}</center></b></td>
        </tr>              
        </tbody>
        </table>`

        $('#search-btn').show()
        $('#btn2').hide()
        $('#searchform')[0].reset()
        }else{
      Swal.fire({
        position: 'top',
        icon: 'error',
        title: 'ไม่พบข้อมูลของคุณ',
        showConfirmButton: false,
        timer: 1500,
      })
      document.getElementById("tb").innerHTML = "";
        $('#search-btn').show()
        $('#btn2').hide()
        }
      }

  </script>
  <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>
  <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.10.2/dist/umd/popper.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.min.js"></script>
  <script src="https://cdn.jsdelivr.net/gh/examblog/web/js/FtExamblog.js"></script>
</body>

</html>
