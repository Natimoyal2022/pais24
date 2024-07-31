<?php session_start();

	include 'conn.php';

  header("Cache-Control: no-store, no-cache, must-revalidate, max-age=0");

  header("Cache-Control: post-check=0, pre-check=0", false);

  header("Pragma: no-cache");



use PHPMailer\PHPMailer\PHPMailer;

use PHPMailer\PHPMailer\Exception;

use PHPMailer\PHPMailer\SMTP;

require 'mailer/Exception.php';

require 'mailer/PHPMailer.php';

require 'mailer/SMTP.php';





if ($_SESSION['loggedin'] == '')

{

	header('location: login.php');

}

else

{









   $x =  date('H:i');





   $v =  explode(":",$x)[1];







  $date = date('Y-m-d');

  if(date('N', strtotime($date)) == '7')

  {



        if($x > '01:00')

        {

          $s= mysqli_query($mysqli,"select * from results where DATE(date) = CURDATE() order by gameTime desc limit 1;");

              $r= mysqli_fetch_assoc($s);



            



            $lastAgrala = $r['agrala'];

        }



      



  }

  if(date('N', strtotime($date)) >= 1 && date('N', strtotime($date)) <=7 )

  {

      $s= mysqli_query($mysqli,"select * from results where DATE(gameTime) = CURDATE() - INTERVAL 1 DAY order by gameTime desc limit 1");

      $r= mysqli_fetch_assoc($s);

      $lastAgrala = $r['agrala'];

  }





  function checkAvail($date,$time)

  {



    if(

      ($date == '2023-09-16' && $time == '23:50') || 

      ($date == '2023-09-16' && $time == '21:30') ||

      ($date == '2023-09-17' && $time == '11:00') || 

      ($date == '2023-09-17' && $time == '13:00') || 

      ($date == '2023-09-17' && $time == '15:00') || 

      ($date == '2023-09-17' && $time == '17:00') || 

      ($date == '2023-09-17' && $time == '19:00') ||

      ($date == '2023-09-17' && $time == '21:00') ||

      ($date == '2023-09-24' && $time == '15:00') ||

      ($date == '2023-09-24' && $time == '17:00') ||

      ($date == '2023-09-24' && $time == '19:00') ||

      ($date == '2023-09-24' && $time == '21:00') ||

      ($date == '2023-09-25' && $time == '11:00') ||

      ($date == '2023-09-25' && $time == '13:00') ||

      ($date == '2023-09-25' && $time == '15:00') ||

      ($date == '2023-09-25' && $time == '17:00') ||

      ($date == '2023-09-25' && $time == '19:00') ||

      ($date == '2023-09-25' && $time == '21:00') ||

      ($date == '2023-09-24' && $time == '11:00') ||

      ($date == '2023-09-24' && $time == '13:00') 

      

      )

      

    {

      return 0;

    }

    else if(

      ($date == '2023-09-17' && $time == '21:30') ||

      ($date == '2023-09-24' && $time == '10:00') ||

      ($date == '2023-09-24' && $time == '12:00') ||

      ($date == '2023-09-25' && $time == '21:30') ||

      ($date == '2023-09-25' && $time == '23:50')

    )

    {

      return 1;

    }

    else

    {

      return 1;

    }



  }

    



//$date =  date('N', strtotime(date('Y-m-d H:i:s')));



include 'headerB.php';



$msg =0;

if ( isset( $_POST['sendit'] ) && $_SESSION['loggedin'] != '' ) {







  



  $user = explode('|',$_POST['user'])[0];



  if ($_POST['temp'] == '1')

	{

    $sql1 = mysqli_query($mysqli,"select * from agentsAdmin where id = '".$_SESSION['loggedin']."'")or die(mysqli_error($mysqli));

    $row1 = mysqli_fetch_assoc($sql1);

    $balance1 = $row1['chanceBalance'];

  }

  else{

        $sql1 = mysqli_query($mysqli,"select * from users where id = '". $user."'")or die(mysqli_error($mysqli));

        $row1 = mysqli_fetch_assoc($sql1);

        $balance1 = $row1['chanceBalance'];

  }

	



  //echo $balance1.' '.$_POST['amount1'];



  for($u=0; $u < $_POST['dup']; $u++)

  {



    $card1 ='';

    $card2 ='';

    $card3 ='';

    $card4 ='';





    echo $balance1. ' '. $_POST['amount1']. ' '.$_POST['total1'];



	if($balance1 -  $_POST['total1'] >= 0)

	{





          $type = 0;

          $am = 0;

		

          $date = date('Y-m-d H:i:s');

          $date = strtotime($date);

          $hour =  date('H:i', $date);

	

					if(isset($_POST['line1']))

					{

						foreach($_POST['line1'] as $l1)

						{

							if($l1 == ''){}

							else{$card1 .= $l1.','; }

						}

						

						$type++;

						

					} else{ $card1 = 0;}

	

					if(isset($_POST['line2']))

					{

						foreach($_POST['line2'] as $l2)

						{

							if($l2 == ''){}

							else{$card2 .= $l2.','; }

						}

						$type++;

						

					} else{ $card2 = 0;}

	

					if(isset($_POST['line3'])){

						

						foreach($_POST['line3'] as $l3)

						{

							if($l3 == ''){}

							else{$card3 .= $l3.','; }

						}

						

						$type++;

						

					} else{ $card3 = 0;}

	

					if(isset($_POST['line4']))

					{

						

						foreach($_POST['line4'] as $l4)

						{

							if($l4 == ''){}

							else{$card4 .= $l4.','; }

						}

						

						$type++;

						

					} else{ $card4 = 0;}

	

	$am = ($_POST['amount1'] / count($_POST['hora']));



  

	foreach($_POST['hora'] as $hourx)

	{

		$hr = explode('-',$hourx);



		if($hour < $hr[0] &&  $hour !== $hr[0])

		{

			if($_POST['type1'] == 2)

			{

				$type = 5;

			}

			if($_POST['type3'] == 3 && $_POST['type1'] == NULL)

			{

				$type = 6;

			}

			if($_POST['type3'] == 3 && $_POST['type1'] == 2)

			{

				$type = 7;

			}

			



			$selection = rtrim($card1,',') . '|' . rtrim($card2,','). '|' . rtrim($card3,',') . '|' . rtrim($card4,',');





      if($am > 0 )

      {





        if ($_POST['temp'] == '1')

        {





         

            mysqli_query( $mysqli, "INSERT INTO `games`( `uid`,`agentId`, `amount`, `selection`, `type`,`gameDate`, `agrala`) VALUES ('0','".$_SESSION['loggedin']."','" . $am . "','" . $selection . "','".$type."','".$hr[0]."','".$hr[1]."')" )or die( mysqli_error( $mysqli ) );

            

          

          $ins = 1;

        }

        else{

          

          mysqli_query( $mysqli, "INSERT INTO `games`( `agentId`,`uid`, `amount`, `selection`, `type`,`gameDate`, `agrala`) VALUES ('".$_POST['agid']."','".$user."','" . $am . "','" . $selection . "','".$type."','".$hr[0]."','".$hr[1]."')" )or die( mysqli_error( $mysqli ) );

          

          

          $ins = 1;

        }



        

			

		



        $send .= '<html><body dir="rtl">-------------------------------------<br>';

        $send .= 'מזהה משתמש :'.$userid.'<br>';

        $send .= 'סכום :'.$am.'<br>';

        $send .= 'בחירה :'.$selection.'<br>';

        $send .= 'סוג  :'.$type.'<br>';

        $send .= 'שעת ההגרלה :'.$hr[0].'<br>';

        $send .= 'תאריך שליחה :'.date('Y-m-d H:i:s').'<br>';

        $send .= 'מספר הגרלה :'.$hr[1].'<br>';

        $send .= '-------------------------------------<br></body</html>';



      $mail = new PHPMailer;                         // TCP port to connect to

      $mail->CharSet = "UTF-8";

      $mail->From = 'tester@pais24.live';

      $mail->FromName = 'Mailer';

      $mail->addAddress('tester@pais24.live', 'User');     // Add a recipient



      $mail->isHTML(true);                                  // Set email format to HTML



      $mail->Subject = 'טופס חדש נשלח';

      $mail->Body    = $send;



      





      }

			

			

		}

		else

		{

			$msg = 1;

		}



	}

    if(!$mail->send()) {

              //echo 'Message could not be sent.';

              //echo 'Mailer Error: ' . $mail->ErrorInfo;

          } else {

              //echo 'Message has been sent';

          }

          

	

	

	

	}else{

		$msg = 3;

	}

}



if($ins == 1)

	{



    if ($_POST['temp'] == '1')

    {

    

      $nb = ($balance1 - $_POST['total1']);

			mysqli_query($mysqli,"update agentsAdmin set `chanceBalance`='".$nb."' where id = '".$_SESSION['loggedin']."'")or die (mysqli_error($mysqli));

      



    }

    else{

    

      $nb = ($balance1 - $_POST['total1']);

			mysqli_query($mysqli,"update users set `chanceBalance`='".$nb."' where id = '".$user."'")or die (mysqli_error($mysqli));

          

    }

		

	

	//header( "location: https://be7.live/pais/mybets.php");

		$url = "mybets.php?st=0";

	echo '<script> window.top.location="' . $url . '"; </script>';

	}

	else

	{

		$msg = 2;

	}



// end of post submit

}

?>



	<style>



    h3{

      text-align: center;

    }

.pb-5, .py-5 {

    padding-bottom: 1rem!important;

}

		

		/* Styling Checkbox Starts */

.checkbox-label {

    display: block;

    position: relative;

    margin: auto;

    cursor: pointer;

    font-size: 12px;

    line-height: 24px;

    height: 24px;

    width: 24px;

    clear: both;

}



.checkbox-label input {

    position: absolute;

    opacity: 0;

    cursor: pointer;

}



.checkbox-label .checkbox-custom {

    position: absolute;

    top: 0px;

    left: 0px;

    height: 24px;

    width: 24px;

    background-color: transparent;

    border-radius: 5px;

  	transition: all 0.3s ease-out;

  	-webkit-transition: all 0.3s ease-out;

  	-moz-transition: all 0.3s ease-out;

  	-ms-transition: all 0.3s ease-out;

  	-o-transition: all 0.3s ease-out;

    border: 2px solid #FFFFFF;

}





.checkbox-label input:checked ~ .checkbox-custom {

    background-color: #FFFFFF;

    border-radius: 5px;

    -webkit-transform: rotate(0deg) scale(1);

    -ms-transform: rotate(0deg) scale(1);

    transform: rotate(0deg) scale(1);

    opacity:1;

    border: 2px solid #FFFFFF;

}





.checkbox-label .checkbox-custom::after {

    position: absolute;

    content: "";

    left: 12px;

    top: 12px;

    height: 0px;

    width: 0px;

    border-radius: 5px;

    border: solid #009BFF;

    border-width: 0 3px 3px 0;

    -webkit-transform: rotate(0deg) scale(0);

    -ms-transform: rotate(0deg) scale(0);

    transform: rotate(0deg) scale(0);

    opacity:1;

  	transition: all 0.3s ease-out;

  	-webkit-transition: all 0.3s ease-out;

  	-moz-transition: all 0.3s ease-out;

  	-ms-transition: all 0.3s ease-out;

  	-o-transition: all 0.3s ease-out;

}





.checkbox-label input:checked ~ .checkbox-custom::after {

  -webkit-transform: rotate(45deg) scale(1);

  -ms-transform: rotate(45deg) scale(1);

  transform: rotate(45deg) scale(1);

  opacity:1;

  left: 8px;

  top: 3px;

  width: 6px;

  height: 12px;

  border: solid #009BFF;

  border-width: 0 2px 2px 0;

  background-color: transparent;

  border-radius: 0;

}







/* For Ripple Effect */

.checkbox-label .checkbox-custom::before {

    position: absolute;

    content: "";

    left: 10px;

    top: 10px;

    width: 0px;

    height: 0px;

    border-radius: 5px;

    border: 2px solid #FFFFFF;

    -webkit-transform: scale(0);

    -ms-transform: scale(0);

    transform: scale(0);	

}



.checkbox-label input:checked ~ .checkbox-custom::before {

    left: -3px;

    top: -3px;

    width: 24px;

    height: 24px;

    border-radius: 5px;

    -webkit-transform: scale(3);

    -ms-transform: scale(3);

    transform: scale(3);

    opacity:0;

    z-index: 999;

    transition: all 0.3s ease-out;

  	-webkit-transition: all 0.3s ease-out;

  	-moz-transition: all 0.3s ease-out;

  	-ms-transition: all 0.3s ease-out;

  	-o-transition: all 0.3s ease-out;

}









/* Style for Circular Checkbox */

.checkbox-label .checkbox-custom.circular {

    border-radius: 40%;

    border: 2px solid #FFFFFF;

}



.checkbox-label input:checked ~ .checkbox-custom.circular {

    background-color: #FFFFFF;

    border-radius: 40%;

    border: 2px solid #FFFFFF;

}

.checkbox-label input:checked ~ .checkbox-custom.circular::after {

    border: solid #0067FF;

    border-width: 0 2px 2px 0;

}

.checkbox-label .checkbox-custom.circular::after {

    border-radius: 40%;

}



.checkbox-label .checkbox-custom.circular::before {

    border-radius: 40%;

    border: 2px solid #FFFFFF;

}



.checkbox-label input:checked ~ .checkbox-custom.circular::before {

    border-radius: 40%;

}





hr {

    border: 0;

    height: 1px;

    background-image: linear-gradient(138deg, #2cda6c, #3e9b90);

}

		

		/* label {

  padding: 3px;

  cursor: pointer;

  display: flex;

  position: relative;

  overflow: hidden;

} */



label input[type="checkbox"] {

  position: absolute;

  clip: rect(1px, 1px, 1px, 1px);

  clip-path: inset(50%);

}



label .icon-box {

  display: flex;

    width: 62px;

    padding: 5px;

    flex-direction: column;

    align-items: center;

    background-color: #4155ee;

    color: #fff;

    border-radius: 3px;

    /* font-size: 15px; */

    transition: 0.5s;

    user-select: none;

}



label input[type="checkbox"]:checked ~ .icon-box {

  background: linear-gradient(138deg, #2cda6c, #3e9b90);

  color: #fff;

}


}



.btn {

  display: inline-block;

    font-weight: 400;

    text-align: center;

    white-space: nowrap;

    vertical-align: middle;

    -webkit-user-select: none;

    -moz-user-select: none;

    -ms-user-select: none;

    user-select: none;

    border: 1px solid transparent;

    padding: 1rem 2.75rem;

    font-size: 12px;

    line-height: 1.5;

    margin: 3px;

    border-radius: 0.25rem;

    transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;

}

		

.btn-group>.btn:first-child {

    margin-left: 3px;

}





		.btn1 {



      -webkit-border-radius: 3px;

    -moz-border-radius: 3px;

    border-radius: -2px;

    font-size: 18px;

    border: 0;

    outline: none;

    transition: 0.5s cubic-bezier(0.755, 0.05, 0.855, 0.06);

    padding: 6px;

}
		.btn2 {



      -webkit-border-radius: 3px;

    -moz-border-radius: 3px;

    border-radius: -2px;

    font-size: 16px;

    border: 0;

    outline: none;

    transition: 0.5s cubic-bezier(0.755, 0.05, 0.855, 0.06);

    padding: 6px;

}



.row{ 

  display: -ms-flexbox;

    display: flex;

    -ms-flex-wrap: wrap;

    flex-wrap: wrap;

    margin-right: 0px;

    margin-left: 0px;

    justify-content: space-evenly;

    padding: 9px;



}
.row2{ 

  display: -ms-flexbox;

    display: flex;

    -ms-flex-wrap: wrap;

    flex-wrap: wrap;

    margin-right: 0px;

    margin-left: 0px;

    justify-content: space-evenly;

    padding: 9px;

}
.row3{ 

  display: -ms-flexbox;

    display: flex;

    -ms-flex-wrap: wrap;

    flex-wrap: wrap;

    margin-right: 0px;

    margin-left: 0px;

    justify-content: space-evenly;

    padding: 9px;

}

.center {
  margin-left: auto;
  margin-right: auto;
}

.c-control {
    margin-left: 0px;
    display: block;
    width: 100%;
    height: calc(3.25rem + 2px);
    padding: 0.375rem 0.75rem;
    font-size: 1.1rem;
    line-height: 1;
    color: #495057;
    background-color: #fff;
    background-clip: padding-box;
    border: 1px solid #ced4da;
    border-radius: 0.75rem;
    transition: border-color .15s ease-in-out,box-shadow .15s ease-in-out;
}


</style>

<div class="userBalance" style="display:none">0</div>

<form method="post" id="fr1" name="fr1">

	<style>
table, th, td {
  border: 0px solid;
text-align: center;
direction: ltr;

}

</style>

<table class="center" overflow-x:auto;  width="95%" border="0" cellspacing="0" cellpadding="0" >
    <tr>
      <th colspan="9">
שליחת טופס חדש
</th>    
</tr>
  <tr>
	<th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

             <input type="checkbox" class="checkbox-input" value="7" name='line1[]' id="trebol7" onClick="cambiarespada(7,'espada',1);" />

              <span class="checkbox-tile"><img src="assets/images/spades.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> 7 </span> </span> </label>

          </div>
</th>    
	<th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

             <input type="checkbox" class="checkbox-input" value="8" name='line1[]' id="trebol7" onClick="cambiarespada(8,'espada',1);" />

              <span class="checkbox-tile"><img src="assets/images/spades.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> 8 </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

             <input type="checkbox" class="checkbox-input" value="9" name='line1[]' id="trebol9" onClick="cambiarespada(9,'espada',1);" />

              <span class="checkbox-tile"><img src="assets/images/spades.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> 9 </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

             <input type="checkbox" class="checkbox-input" value="10" name='line1[]' id="trebol7" onClick="cambiarespada(10,'espada',1);" />

              <span class="checkbox-tile"><img src="assets/images/spades.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> 10 </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

             <input type="checkbox" class="checkbox-input" value="11" name='line1[]' id="trebol7" onClick="cambiarespada(11,'espada',1);" />

              <span class="checkbox-tile"><img src="assets/images/spades.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> J </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

             <input type="checkbox" class="checkbox-input" value="12" name='line1[]' id="trebol7" onClick="cambiarespada(12,'espada',1);" />

              <span class="checkbox-tile"><img src="assets/images/spades.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> Q </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

             <input type="checkbox" class="checkbox-input" value="13" name='line1[]' id="trebol7" onClick="cambiarespada(13,'espada',1);" />

              <span class="checkbox-tile"><img src="assets/images/spades.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> K </span> </span> </label>

          </div>
</th>
   <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

             <input type="checkbox" class="checkbox-input" value="1" name='line1[]' id="trebol7" onClick="cambiarespada(1,'espada',1);" />

              <span class="checkbox-tile"><img src="assets/images/spades.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> A </span> </span> </label>

          </div>
</th>

        <th rowspan="8" width="30%"  style="text-align:center;   vertical-align: top;">

  <div class="col-2A" style="padding:4px;   vertical-align: top;">


  <!-- <div class="btn-group btn-group-toggle" data-toggle="buttons">

  <label class="btn btn-secondary">

    <input type="checkbox" autocomplete="off"> Check

  </label>

</div> -->


<?php

$s3=mysqli_query($mysqli,"select * from users where agentId = '".$_SESSION['id']."'");

$r3=mysqli_num_rows($s3);


?>

  <div class="row">

<input type="hidden" name="agid" value="<?=$_SESSION['loggedin']?>">
<div class="col-md-12">

<div align="center" class="userBalance"></div>

</div>

  <div class="cat action" style="margin-left: 0px;">

   <label>

      <input type="checkbox" name="temp" value="1" class="tmpp"><span class="temp">
משתמש זמני

</span>

   </label>

</div>
<div class="col-md-12">


</div>
    <div class="btn-group" style="text-align:center">

  <select name="user" class="c-control userSelect" require>

   <option value="">  שם משתמש </option>

  <div class="dropdown-menu">

  <?php

while($f3=mysqli_fetch_assoc($s3))

{

?>

<option value="<?=$f3['id']?>|<?=$f3['chanceBalance']?>"> <?=$f3['username']?></option>
<br><br>
    <?php } ?>

</select>

  </div>



</fieldset>

 <div class="" style="text-align:center">
<br>
<h3>שעת הגרלה</h3>			  
 <?php



if($lastAgrala != '')

{

$date = date('Y-m-d H:i:s');

$date = strtotime($date);

$hour =  date('H:i', $date);

$minute =  date('i', $date);



                  ?>



<?php $date = date('Y-m-d H:i:s');

if((($hour < '10:00')  && date('N', strtotime($date)) == 5) ){?>



<label tabindex="0">

<input tabindex="-1" type="checkbox" name="hora[]" value="10:00-<?php echo $lastAgrala + 1; ?>" class="hora10 hora"  style="display:none"/>

 

<div class="icon-box h10">

<?php echo $lastAgrala + 1;?>

<span>10:00</span>

</div>

</label>



                  <?php } ?>



<?php $date = date('Y-m-d H:i:s');

if((($hour < '12:00')  && date('N', strtotime($date)) == 5)){?>



<label tabindex="0">

<input tabindex="-1" type="checkbox" name="hora[]" value="12:00-<?php echo $lastAgrala + 2; ?>" class="hora12 hora"  style="display:none"/>

 

<div class="icon-box h12">

<?php echo $lastAgrala + 2;?>

<span>12:00</span>

</div>

</label>



                  <?php } ?>



      <?php $date = date('Y-m-d H:i:s');

if((($hour < '14:00')  && date('N', strtotime($date)) == 5)  && checkAvail(date('Y-m-d'),'14:00') == 1){?>



<label tabindex="0">

<input tabindex="-1" type="checkbox" name="hora[]" value="14:00-<?php echo $lastAgrala + 3; ?>" class="hora14 hora"  style="display:none"/>

 

<div class="icon-box h14">

<?php echo $lastAgrala + 3;?>

<span>14:00</span>

</div>

</label>



                  <?php } ?>







<?php $date = date('Y-m-d H:i:s');

if(((($hour < '11:00')  && date('N', strtotime($date)) != 6  && date('N', strtotime($date)) != 5))  && checkAvail(date('Y-m-d'),'11:00') == 1){?>



<label tabindex="0">

<input tabindex="-1" type="checkbox" name="hora[]" value="11:00-<?php echo $lastAgrala + 1; ?>" class="hora11 hora"  style="display:none"/>

 

<div class="icon-box h11">

<?php echo $lastAgrala + 1;?>

<span>11:00</span>

</div>

</label>



                  <?php } ?>

                  

<?php $date = date('Y-m-d H:i:s');

if((($hour < '13:00' ) && date('N', strtotime($date)) != 6  && date('N', strtotime($date)) != 5)  && checkAvail(date('Y-m-d'),'13:00') == 1){?>



                  <label tabindex="0">

<input tabindex="-1" type="checkbox" name="hora[]" value="13:00-<?php echo $lastAgrala + 2; ?>" class="hora13 hora"  style="display:none"/>

                      

<div class="icon-box h13">

<?php echo $lastAgrala + 2; ?>

<span>13:00</span>

</div>

</label>



                  <?php } ?>

      <?php $date = date('Y-m-d H:i:s');

if((($hour < '15:00' ) && date('N', strtotime($date)) != 6  && date('N', strtotime($date)) != 5) && checkAvail(date('Y-m-d'),'15:00') == 1){?>



                  <label tabindex="0">

<input tabindex="-1" type="checkbox" name="hora[]" value="15:00-<?php echo $lastAgrala + 3;?>" class="hora17 hora"  style="display:none"/>

                    

                      

<div class="icon-box h15">

<?php echo $lastAgrala + 3; ?>

<span>15:00</span>

</div>

</label>



                  <?php } ?>







<?php $date = date('Y-m-d H:i:s');

if((($hour < '17:00' ) && date('N', strtotime($date)) != 6  && date('N', strtotime($date)) != 5)  && checkAvail(date('Y-m-d'),'17:00') == 1){?>



                  <label tabindex="0">

<input tabindex="-1" type="checkbox" name="hora[]" value="17:00-<?php echo $lastAgrala + 4; ?>" class="hora17 hora"  style="display:none"/>

                    

                      

<div class="icon-box h17">

<?php echo $lastAgrala + 4; ?>

<span>17:00</span>

</div>

</label>



                  <?php } ?>

                  

<?php $date = date('Y-m-d H:i:s');

if((($hour < '19:00' ) && date('N', strtotime($date)) != 6 && date('N', strtotime($date)) != 5)  && checkAvail(date('Y-m-d'),'19:00') == 1){?>





                  <label tabindex="0">

<input tabindex="-1" type="checkbox" name="hora[]" value="19:00-<?php echo $lastAgrala + 5; ?>" class="hora19 hora"  style="display:none"/>

                    

                      

<div class="icon-box h19">

<?php echo $lastAgrala + 5; ?>

<span>19:00</span>

</div>

</label><?php } ?>

                  

<?php $date = date('Y-m-d H:i:s');





if(((($hour < '21:00' ) && date('N', strtotime($date)) != 6 && date('N', strtotime($date)) != 5)  && checkAvail(date('Y-m-d'),'21:00') == 1))

{

?>

                  <label tabindex="0">

<input tabindex="-1" type="checkbox" name="hora[]" value="21:00-<?php echo $lastAgrala + 6; ?>" class="hora21 hora"  style="display:none"/>

                    

                      

<div class="icon-box h21">

<?php echo $lastAgrala + 6; ?>

<span>21:00</span>

</div>

</label><?php } ?>				  



<?php

$date = date('Y-m-d H:i:s');

if(($hour < '21:30' &&  date('N', strtotime($date)) == 6)  )

{

  ?>

  <label tabindex="0">

      <input tabindex="-1" type="checkbox" name="hora[]" value="21:30-<?php echo $lastAgrala + 1; ?>" class="hora213 hora"  style="display:none"/>

	

      <div class="icon-box 213">

       

        <span>21:30</span>

      </div>

    </label>	

    <?php 

  } 

  ?>



						  <?php

$date = date('Y-m-d H:i:s');

if(($hour < '23:50' &&  date('N', strtotime($date)) == 6) )

{

  ?><label tabindex="0">

      <input tabindex="-1" type="checkbox" name="hora[]" value="23:50-<?php echo $lastAgrala + 2; ?>" class="hora23 hora"  style="display:none"/>

	

      <div class="icon-box h235">

       

        <span> 23:50 </span>

      </div>

    </label>

						  

    <?php 

  } 
else
{
echo ' אין יותר הגרלות להיום ';
}
} 

  ?>
						  
             	 <input type="hidden" class="amount1" name="amount1" value="">
<br><br>
<h3>סכום</h3>
<div class="col-md-12">

      <input class="checkbox-budget" type="radio" name="amount" id="budget-1" value="5">

      <label class="for-checkbox-budget" for="budget-1"> <span data-hover="₪5">₪5</span> </label>



    

      <input class="checkbox-budget" type="radio" name="amount" id="budget-2" value="10">

      <label class="for-checkbox-budget" for="budget-2"> <span data-hover="₪10">₪10</span> </label>





    

      <input class="checkbox-budget" type="radio" name="amount" id="budget-3" value="25">

      <label class="for-checkbox-budget" for="budget-3"> <span data-hover="₪25">₪25</span> </label>





<br> 

      <input class="checkbox-budget" type="radio" name="amount" id="budget-4" value="50">

      <label class="for-checkbox-budget" for="budget-4"> <span data-hover="₪50">₪50</span> </label>





    

      <input class="checkbox-budget" type="radio" name="amount" id="budget-5" value="70">

      <label class="for-checkbox-budget" for="budget-5"> <span data-hover="₪70">₪70</span> </label>



    

      <input class="checkbox-budget" type="radio" name="amount" id="budget-6" value="100">

      <label class="for-checkbox-budget" for="budget-6"> <span data-hover="₪100">₪100</span> </label>





    </div>  

    <div class="form-outline">

  <h3>  עותקים</h3> 

    <input class="numberstyle dups" type="number" min="1" step="1" value="1" name="dup">

  </div>

  <div class="col-s2" style="padding:4px;">



  <!-- <div class="btn-group btn-group-toggle" data-toggle="buttons">

 

  <label class="btn btn-secondary1">

    <input type="checkbox" autocomplete="off"> Check

  </label>

</div> -->


<?php

$s3=mysqli_query($mysqli,"select * from users where agentId = '".$_SESSION['id']."'");

$r3=mysqli_num_rows($s3);


?>

</th>
  </tr>
  
  <tr>
  
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="7" name='line2[]' id="trebol7" onClick="cambiarespada(7,'corazon',2);" />

              <span class="checkbox-tile img1"><img src="assets/images/hearth.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> 7 </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="8" name='line2[]' id="trebol7" onClick="cambiarespada(8,'corazon',2);" />

              <span class="checkbox-tile img1"><img src="assets/images/hearth.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> 8 </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="9" name='line2[]' id="trebol7" onClick="cambiarespada(9,'corazon',2);" />

              <span class="checkbox-tile img1"><img src="assets/images/hearth.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> 9 </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

             <input type="checkbox" class="checkbox-input" value="10" name='line2[]' id="trebol7" onClick="cambiarespada(10,'corazon',2);" />

              <span class="checkbox-tile"><img src="assets/images/hearth.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> 10 </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="11" name='line2[]' id="trebol7" onClick="cambiarespada(11,'corazon',2);" />

              <span class="checkbox-tile img1"><img src="assets/images/hearth.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> J </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="12" name='line2[]' id="trebol7" onClick="cambiarespada(12,'corazon',2);" />

              <span class="checkbox-tile img1"><img src="assets/images/hearth.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> Q </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

             <input type="checkbox" class="checkbox-input" value="13" name='line2[]' id="trebol7" onClick="cambiarespada(13,'corazon',2);" />

              <span class="checkbox-tile"><img src="assets/images/hearth.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> K </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

             <input type="checkbox" class="checkbox-input" value="1" name='line2[]' id="trebol7" onClick="cambiarespada(1,'corazon',2);" />

              <span class="checkbox-tile"><img src="assets/images/hearth.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> A </span> </span> </label>

          </div>
</th>

  </tr>

  
  <tr>
       <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="7" name='line3[]' id="trebol7" onClick="cambiarespada(7,'diamante',3);" />

              <span class="checkbox-tile img1"><img src="assets/images/diamonds.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> 7 </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="8" name='line3[]' id="trebol7" onClick="cambiarespada(8,'diamante',3);" />

              <span class="checkbox-tile img1"><img src="assets/images/diamonds.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> 8 </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="9" name='line3[]' id="trebol7" onClick="cambiarespada(9,'diamante',3);" />

              <span class="checkbox-tile img1"><img src="assets/images/diamonds.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> 9 </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="10" name='line3[]' id="trebol7" onClick="cambiarespada(10,'diamante',3);" />

              <span class="checkbox-tile img1"><img src="assets/images/diamonds.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> 10 </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="11" name='line3[]' id="trebol7" onClick="cambiarespada(11,'diamante',3);" />

              <span class="checkbox-tile img1"><img src="assets/images/diamonds.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> J </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="12" name='line3[]' id="trebol7" onClick="cambiarespada(12,'diamante',3);" />

              <span class="checkbox-tile img1"><img src="assets/images/diamonds.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> Q </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="13" name='line3[]' id="trebol7" onClick="cambiarespada(13,'diamante',3);" />

              <span class="checkbox-tile img1"><img src="assets/images/diamonds.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> K </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="1" name='line3[]' id="trebol7" onClick="cambiarespada(1,'diamante',3);" />

              <span class="checkbox-tile img1"><img src="assets/images/diamonds.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> A </span> </span> </label>

          </div>
</th>
</tr>

<tr>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="7" name='line4[]' id="trebol7" onClick="cambiarespada(7,'trebol',4);" />

              <span class="checkbox-tile img1"><img src="assets/images/clubs.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> 7 </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="8" name='line4[]' id="trebol7" onClick="cambiarespada(8,'trebol',4);" />

              <span class="checkbox-tile img1"><img src="assets/images/clubs.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> 8 </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="9" name='line4[]' id="trebol7" onClick="cambiarespada(9,'trebol',4);" />

              <span class="checkbox-tile img1"><img src="assets/images/clubs.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> 9 </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="10" name='line4[]' id="trebol7" onClick="cambiarespada(10,'trebol',4);" />

              <span class="checkbox-tile img1"><img src="assets/images/clubs.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> 10 </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="11" name='line4[]' id="trebol7" onClick="cambiarespada(11,'trebol',4);" />

              <span class="checkbox-tile img1"><img src="assets/images/clubs.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> J </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="12" name='line4[]' id="trebol7" onClick="cambiarespada(12,'trebol',4);" />

              <span class="checkbox-tile img1"><img src="assets/images/clubs.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> Q </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="13" name='line4[]' id="trebol7" onClick="cambiarespada(13,'trebol',4);" />

              <span class="checkbox-tile img1"><img src="assets/images/clubs.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> K </span> </span> </label>

          </div>
</th>
    <th rowspan="1">
<div class="checkbox">

            <label class="checkbox-wrapper">

              <input type="checkbox" class="checkbox-input" value="1" name='line4[]' id="trebol7" onClick="cambiarespada(1,'trebol',4);" />

              <span class="checkbox-tile img1"><img src="assets/images/clubs.png" width="27" height="30" alt=""/> <span class="checkbox-icon"> A </span> </span> </label>

          </div>
</th>



</tr>
        <tr>
    <th rowspan="1" colspan="8">
<div  class="row2" style="padding: 0px; line-height: 2;  font-size: 16px;  text-align: center;">

<div class="col-md-3"> רב צאנס <input type="checkbox" name="type1" value="2" id="type1"></div>    

<div class="col-md-3"> טופס שיטתי <input type="checkbox" name="type3" value="3" id="type2"></div>

</th>
  </tr>
        <tr>   

    <th rowspan="1" colspan="8" >
<div  class="row3" style="padding: 0px; line-height: 2;  font-size: 16px;  text-align: center;">


<div class="col-md-3">
<table width="100%" border="0" cellspacing="0" cellpadding="0" id="calc" style="display: none; background-color: #efefef;">


    <tr> 
 <td  id="calcw">0</td>
      <td>:מספר צירופים</td>

    </tr>

</table>
</div>
</div>
</th>
  </tr>
          <tr>   
    <th rowspan="1" colspan="8">
    <div class="row" style="padding: 0px; line-height: 2;  font-size: 16px;  text-align: center;">

    <input type="hidden" class="amount1" name="amount1" value=""> 

    <input type="hidden" class="total1" name="total1" value="">

	<div class="col-md-3" style="margin-top: 0px;"> ₪ <span class="total" style="font-size: 24px; color:#e85959">0</span>  <span  style="font-size: 18px;">לתשלום</span></div> 

	<div class="col-md-3"><input class="btn1 btn-success" type="submit" name="sendit" value="שלח טופס"  id="checkBtn"></div>  

	<div class="col-md-3"><label><input class="btn1 btn-info" type="button" value="מילוי אוטומטי" style="font-weight: bold;" id="lucky" /> </label></div>

	<div class="col-md-3"><input class="btn1" type="reset"" value="נקה טופס" style="background-color: #d30404; color: #ffffff";  font-weight: bold;"></div>  

    </div>
</th>

  </tr>
    

<div class="container">



<p style="color:crimson"><?php if($msg == 1){echo 'שעת המשחק עברה';}?></p>

<p style="color:crimson"><?php if($msg == 3){echo 'יתרה לא מאפשרת ';}?></p>



    




              <script>

 function check(input)

    {

    	

    	var checkboxes = document.getElementsByClassName("radioCheck");

    	

    	for(var i = 0; i < checkboxes.length; i++)

    	{

    		//uncheck all

    		if(checkboxes[i].checked == true)

    		{

    			checkboxes[i].checked = false;

    		}

    	}

    	

    	//set checked of clicked object

    	if(input.checked == true)

    	{

    		input.checked = false;

    	}

    	else

    	{

    		input.checked = true;

    	}	

    }

    </script>









<script>

																// the selector will match all input controls of type :checkbox

// and attach a click event handler 





$(".checkbox input:checkbox").on('click', function() {





  // in the handler, 'this' refers to the box clicked on

	if(!$('#type2').is(':checked'))

		{

			var $box = $(this);

		  if ($box.is(":checked")) {

			// the name of the box is retrieved using the .attr() method

			// as it is assumed and expected to be immutable

			var group = "input:checkbox[name='" + $box.attr("name") + "']";

			// the checked state of the group/box on the other hand will change

			// and the current value is retrieved using .prop() method

			$(group).prop("checked", false);

			$box.prop("checked", true);

		  } else {

			$box.prop("checked", false);

		  }

		}

	else{

		

	}

  



});

$("#type2").on('click', function() {

	

	$(".checkbox-input").prop('checked', false); 

	$(".checkbox-budget").prop('checked', false); 

	// $('#cardimg').toggle();

	// $('#calc').toggle();

	

	// $('#allamounts').toggle();



  if($('#type2').prop('checked') == true)

  {

    $('#allamounts').hide();

    $('#cardimg').hide();

    $('#calc').show();

  }



  if($('#type1').prop('checked') == true && $('#type2').prop('checked') == false)

  {

    $('#allamounts').show();

    $('#cardimg').show();

    $('#calc').hide();

  }



  if($('#type1').prop('checked') == true && $('#type2').prop('checked') == true)

  {

    $('#allamounts').hide();

    $('#cardimg').hide();

    $('#calc').show();

  }



  if($('#type1').prop('checked') == false && $('#type2').prop('checked') == false)

  {

    $('#allamounts').show();

    $('#cardimg').show();

    $('#calc').hide();

  }



});





$("#type1").on('click', function() {



  console.log($('#type1').prop('checked'));

  console.log($('#type2').prop('checked'));

	

	$(".checkbox-input").prop('checked', false); 

	$(".checkbox-budget").prop('checked', false); 

	//$('#cardimg').show();

	// $('#calc').toggle();

	

  if($('#type2').prop('checked') == true)

  {

    $('#allamounts').hide();

    $('#cardimg').hide();

    $('#calc').show();

  }



  if($('#type1').prop('checked') == true && $('#type2').prop('checked') == true)

  {

    $('#allamounts').hide();

    $('#cardimg').hide();

    $('#calc').show();

  }



  if($('#type1').prop('checked') == false && $('#type2').prop('checked') == false)

  {

    $('#allamounts').show();

    $('#cardimg').show();

    $('#calc').hide();

  }

	



});

	

$('[name="line1[]"]').change(function(){

    var max= 4;

    if( $('[name="line1[]"]:checked').length == max ){

        $('[name="line1[]"]').attr('disabled', 'disabled');

        $('[name="line1[]"]:checked').removeAttr('disabled');

    }else{

         $('[name="line1[]"]').removeAttr('disabled');

    }

})

	

$('[name="line2[]"]').change(function(){

    var max= 4;

    if( $('[name="line2[]"]:checked').length == max ){

        $('[name="line2[]"]').attr('disabled', 'disabled');

        $('[name="line2[]"]:checked').removeAttr('disabled');

    }else{

         $('[name="line2[]"]').removeAttr('disabled');

    }

})

	

$('[name="line3[]"]').change(function(){

    var max= 4;

    if( $('[name="line3[]"]:checked').length == max ){

        $('[name="line3[]"]').attr('disabled', 'disabled');

        $('[name="line3[]"]:checked').removeAttr('disabled');

    }else{

         $('[name="line3[]"]').removeAttr('disabled');

    }

})

	

$('[name="line4[]"]').change(function(){

    var max= 4;

    if( $('[name="line4[]"]:checked').length == max ){

        $('[name="line4[]"]').attr('disabled', 'disabled');

        $('[name="line4[]"]:checked').removeAttr('disabled');

    }else{

         $('[name="line4[]"]').removeAttr('disabled');

    }

})

	



		

		function cambiarespada(numero,c,cart){

						

			if(cart == 1)

				{

					

					document.getElementById("carta1").src="assets/images/"+c+""+numero+".png?v=<?=$v?>";

				}

			if(cart == 2)

				{

	

					document.getElementById("carta2").src="assets/images/"+c+""+numero+".png?v=<?=$v?>";

				}

			if(cart == 3)

				{

				

					document.getElementById("carta3").src="assets/images/"+c+""+numero+".png?v=<?=$v?>";

				}

			if(cart == 4)

				{

		

					document.getElementById("carta4").src="assets/images/"+c+""+numero+".png?v=<?=$v?>";

				}

					    



						  



						

					}

					

					

					

function aleatorio1(inferior, superior) {

    var numPosibilidades = superior - inferior;

    var aleatorio = Math.random() * (numPosibilidades + 1);

    aleatorio = Math.floor(aleatorio);

    return inferior + aleatorio;

}

					

$("#fr1").submit(function (e) {

  var t1;

    var t2;



   // e.preventDefault();

    var g1 = $('[name="line1[]"]:checked').length;

    var g2 = $('[name="line2[]"]:checked').length;

    var g3 = $('[name="line3[]"]:checked').length;

    var g4 = $('[name="line4[]"]:checked').length;

	

    t1 = $('[name="type1"]:checked').length;

    t2 = $('[name="type3"]:checked').length;

	

    var amount = $('.checkbox-budget[name=amount]:checked').length;

	

	var atLeastOneIsChecked = $('input[name="hora[]"]:checked').length > 0;

	



  if(!$('.tmpp').is(':checked') && $('.userSelect').val() == ''){

    //&& $('.userSelect').val() == ''

    alert('נא לבחור משתמש');

    return false;

}



    if ((g1 + +g2 + +g3 + +g4) < 1)

		{

		  alert('נא לבחור לפחות קלף 1');

			return false;

		}



    

	if (t1 > 0 && (+g1 == 0 || +g2 == 0 || +g3 == 0 || +g4 == 0))

		{

		  alert('חובה לבחור 4 קלפים');

			return false;

		}

	if ( atLeastOneIsChecked < 1)

		{

		  alert('נא לבחור שעת הגרלה');

			return false;

		}

	if (amount < 1)

		{

			alert('נא לבחור סכום הימור');

			return false;

		}

	if ((parseInt($('.userBalance').text()) - parseInt($('.total1').text())) < 0)

		{

      console.log( parseInt($('.userBalance').text()) , parseInt($('.total').text()));

			alert('יתרה לא מאפשרת' );

			return false;

		}

	else{



    var be;

    var what;

		

		if((g1 + +g2 + +g3 + +g4) == 1){be = 'צאנס 1';}

		if((g1 + +g2 + +g3 + +g4) == 2){be = 'צאנס 2';}

		if((g1 + +g2 + +g3 + +g4) == 3){be = 'צאנס 3';}

		if((g1 + +g2 + +g3 + +g4) == 4){be = 'צאנס 4';}





    var amountit=0;



    if((g1) >= 1){++amountit;}

		if((g2) >= 1){++amountit;}

		if((g3) >= 1){++amountit;}

		if((g4) >= 1){++amountit;}







		

		if(t1 == 1){be = ' רב צאנס';}

		if(t2 == 1){be = 'שיטה צאנס ' + amountit;}

		if(t2 == 1 && t1 == 1 ){be = ' שיטה רב צאנס';}

		

		if (confirm(' סוג ההימור שאתה שולח הוא '+be+' האם לשלוח?')) {

           fr1.submit();

			alert('הטופס נשלח, בהצלחה!');

       } else {

           return false;

       }



	}

        

});

		

	

	// function limpio(numero){

	// //	alert('hola');

		

	// 		document.getElementById("carta"+numero).src="assets/images/card-back.png";

		 	

	// 	 $('.checkbox-input[name=line'+numero+']').prop('checked',false);



		

	// }

	

function getRand(exclude, max)

{

    var dupe = true;

    var myRandom;

    

    while(dupe)

    {

        myRandom = Math.floor(Math.random() * max);

        

        var found = false;

        for(var i=0;i<exclude.length; i++)

        {

            if(myRandom == exclude[i])

            {

                found = true;   

            }

        }

        

        if(!found) dupe = false;

    }

    

    return myRandom;

}



window.onload = function(){

    

    document.getElementById("lucky").onclick = function(){



        var checkboxList1 = document.getElementsByName("line1[]");

        var checkboxList2 = document.getElementsByName("line2[]");

        var checkboxList3 = document.getElementsByName("line3[]");

        var checkboxList4 = document.getElementsByName("line4[]");

		

        var rands1 = [];

        var rands2 = [];

        var rands3 = [];

        var rands4 = [];

        

        var total = 1;

        

        for(var j=0; j<checkboxList1.length; j++){ checkboxList1[j].checked = false; }

        for(var j=0; j<checkboxList2.length; j++){ checkboxList2[j].checked = false; }

        for(var j=0; j<checkboxList3.length; j++){ checkboxList3[j].checked = false; }

        for(var j=0; j<checkboxList4.length; j++){ checkboxList4[j].checked = false; }

        

		var c1;

		var c2;

		var c3;

		var c4;

		var c5 = [7,8,9,10,11,12,13,1];

        for(var i=0; i<total; i++)

        {

            var myRandom = getRand(rands1, checkboxList1.length);

			c1  = myRandom;

            rands1.push(myRandom);

        }

        

        for(var x=0; x<rands1.length; x++)

        {

            checkboxList1[rands1[x]].checked = true;

			//document.getElementById("carta1").src="assets/images/espada"+c5[c1]+".png?v=<?=$v?>";

        }

		

		

		for(var i=0; i<total; i++)

        {

            var myRandom = getRand(rands2, checkboxList2.length);

			c2  = myRandom;

            rands2.push(myRandom);

        }

        

        for(var x=0; x<rands2.length; x++)

        {

            checkboxList2[rands2[x]].checked = true;  

			//document.getElementById("carta2").src="assets/images/corazon"+c5[c2]+".png?v=<?=$v?>";

        }

		

		for(var i=0; i<total; i++)

        {

			

            var myRandom = getRand(rands3, checkboxList3.length);

			c3  = myRandom;

            rands3.push(myRandom);

        }

        

        for(var x=0; x<rands3.length; x++)

        {

            checkboxList3[rands3[x]].checked = true;

			//document.getElementById("carta3").src="assets/images/diamante"+c5[c3]+".png?v=<?=$v?>";

        }

		

		

		for(var i=0; i<total; i++)

        {

			

            var myRandom = getRand(rands4, checkboxList4.length);

			c4  = myRandom;

            rands4.push(myRandom);

        }

        

        for(var x=0; x<rands4.length; x++)

        {

            checkboxList4[rands4[x]].checked = true;

			//document.getElementById("carta4").src="assets/images/trebol"+c5[c4]+".png?v=<?=$v?>";

        }

        

    };        

    

};

				</script>



<script>

function myFunction() {

  var d = new Date();

  var n = d.getHours();

  var k = d.getMinutes();

  var o = d.getSeconds();



 

 if(o < '10'){ var ox = '0' + o;} else {ox = o;}

 if(k < '10'){ var kx = '0' + k;} else {kx = k;}

 if(n < '10'){ var nx = '0' + n;} else {nx = n;}

	

  $(".timer").html(nx + ':' + kx + ':' + ox);

	 //console.log(nx + ':' + kx + ':' + ox);

	//console.log(nx + ':' + kx);

	if((nx +':'+ kx) < '10:00')

		{

			$('.h10').show();

			//console.log(kx +':'+ ox);

			//console.log('its ok');

		} else {$('.h10').hide();}



    if((nx +':'+ kx) < '12:00')

		{

			$('.h12').show();

			//console.log(kx +':'+ ox);

			//console.log('its ok');

		} else {$('.h12').hide();}



    if((nx +':'+ kx) < '14:00')

		{

			$('.h14').show();

			//console.log(kx +':'+ ox);

			//console.log('its ok');

		} else {$('.h14').hide();}

    

    if((nx +':'+ kx) < '11:00')

		{

			$('.h11').show();

			//console.log(kx +':'+ ox);

			//console.log('its ok');

		} else {$('.h11').hide();}





	if((nx +':'+ kx) < '13:00')

		{

			$('.h13').show();

			//console.log(kx +':'+ ox);

			//console.log('its ok');

		} else {$('.h13').hide();}





	if((nx +':'+ kx) < '15:00')

		{

			$('.h15').show();

			//console.log(kx +':'+ ox);

			//console.log('its ok');

		} else {$('.h15').hide();}







	if((nx +':'+ kx) < '17:00' || (nx +':'+ kx) > '0:00')

		{

			$('.hora17').show();

			//console.log(kx +':'+ ox);

			//console.log('its ok');

		} else {$('.hora17').hide();}

	

	if((nx +':'+ kx) < '19:00')

		{

			$('.h19').show();

			//console.log(kx +':'+ ox);

			//console.log('its ok');

		} else {$('.h19').hide();}







	if((nx +':'+ kx) < '21:00')

		{

			$('.h21').show();

		} else {$('.h21').hide();}





	if((nx +':'+ kx) < '21:30')

		{

			$('.hora213').show();



		} else {$('.h213').hide();}

	

	if((nx +':'+ kx) < '23:50')

		{

			$('.h235').show();



		} else {$('.h235').hide();}

	

	if ($('.checkbox-budget').is(":checked"))

{



	var m1 = $('[name="line1[]"]:checked').length;

	var m2 = $('[name="line2[]"]:checked').length;

	var m3 = $('[name="line3[]"]:checked').length;

	var m4 = $('[name="line4[]"]:checked').length;

	

	if(m1 > 1){ m1 = m1;}else{ m1 = 1;}

	if(m2 > 1){ m2 = m2;}else{ m2 = 1;}

	if(m3 > 1){ m3 = m3;}else{ m3 = 1;}

	if(m4 > 1){ m4 = m4;}else{ m4 = 1;}

	

	var multi = (m1  * m2 * m3 * m4);

	$('#calcw').text(multi);

	$('.total').html($('.checkbox-budget:checked').val() * $('.hora:checked').length * multi * ($('.dups').val()));

	$('.total1').val($('.checkbox-budget:checked').val() * $('.hora:checked').length * multi * ($('.dups').val()));

	$('.amount1').val($('.checkbox-budget:checked').val() * $('.hora:checked').length * multi);

}

	

	

}

setInterval(myFunction, 1000);



(function( $ ) {



$.fn.numberstyle = function(options) {



  /*

   * Default settings

   */

  var settings = $.extend({

    value: 0,

    step: undefined,

    min: undefined,

    max: undefined

  }, options );



  /*

   * Init every element

   */

  return this.each(function(i) {

      

    /*

     * Base options

     */

    var input = $(this);

        

    /*

     * Add new DOM

     */

    var container = document.createElement('div'),

        btnAdd = document.createElement('div'),

        btnRem = document.createElement('div'),

        min = (settings.min) ? settings.min : input.attr('min'),

        max = (settings.max) ? settings.max : input.attr('max'),

        value = (settings.value) ? settings.value : parseFloat(input.val());

    container.className = 'numberstyle-qty';

    btnAdd.className = (max && value >= max ) ? 'qty-btn qty-add disabled' : 'qty-btn qty-add';

    btnAdd.innerHTML = '+';

    btnRem.className = (min && value <= min) ? 'qty-btn qty-rem disabled' : 'qty-btn qty-rem';

    btnRem.innerHTML = '-';

    input.wrap(container);

    input.closest('.numberstyle-qty').prepend(btnRem).append(btnAdd);



    /*

     * Attach events

     */

    // use .off() to prevent triggering twice

    $(document).off('click','.qty-btn').on('click','.qty-btn',function(e){

      

      var input = $(this).siblings('input'),

          sibBtn = $(this).siblings('.qty-btn'),

          step = (settings.step) ? parseFloat(settings.step) : parseFloat(input.attr('step')),

          min = (settings.min) ? settings.min : ( input.attr('min') ) ? input.attr('min') : undefined,

          max = (settings.max) ? settings.max : ( input.attr('max') ) ? input.attr('max') : undefined,

          oldValue = parseFloat(input.val()),

          newVal;

      

      //Add value

      if ( $(this).hasClass('qty-add') ) {   

        

        newVal = (oldValue >= max) ? oldValue : oldValue + step,

        newVal = (newVal > max) ? max : newVal;

        

        if (newVal == max) {

          $(this).addClass('disabled');

        }

        sibBtn.removeClass('disabled');

       

      //Remove value

      } else {

        

        newVal = (oldValue <= min) ? oldValue : oldValue - step,

        newVal = (newVal < min) ? min : newVal; 

        

        if (newVal == min) {

          $(this).addClass('disabled');

        }

        sibBtn.removeClass('disabled');

        

      }

        

      //Update value

      input.val(newVal).trigger('change');

          

    });

    

    input.on('change',function(){

      

      const val = parseFloat(input.val()),

            min = (settings.min) ? settings.min : ( input.attr('min') ) ? input.attr('min') : undefined,

            max = (settings.max) ? settings.max : ( input.attr('max') ) ? input.attr('max') : undefined;

      

      if ( val > max ) {

        input.val(max);   

      }

      

      if ( val < min ) {

        input.val(min);

      }

    });

    

  });

};





/*

 * Init

 */



$('.numberstyle').numberstyle();



}( jQuery ));





$('.temp').click(function()

{

  console.log('clicked');

  $('.userSelect').toggle();

});





$('.userSelect').change(function(e)

{

  var vl = $(this).val().split('|')[1];

  

  $('.userBalance').text('יתרה לשחקן '+vl);

})





// $('.dups').change(function(e)

// {

//   var vl = $(this).val();

//   console.log(vl);



//   $('.total').text(parseInt($('.total').text()) * vl);





// })











</script>

<?php

include( 'footer.php' );

}

?>


</table>

    </div>

  </div>

</div>    

</div>    




</body>
</html>
        



    
