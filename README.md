# PRNTSET
Printer Settings


@echo off
TITLE : : : : ESH SITE MACHINE SETUP : : : :
:START
TITLE 	YOU ARE SETTING UP A SITE MACHINE FOR AN EXTENDED STAY HOTEL
COLOR 4A



:: ::::::::::::::::::::::::::::::::::::::::::::::::::::::
:: These are the known common ESH Site Printer Types
:: and are onlyhere for informational purposes
:: ::::::::::::::::::::::::::::::::::::::::::::::::::::::
::   HP LaserJet 2200
::   HP LaserJet 4000 series
::   HP LaserJet 4
::   HP LaserJet 5
::   HP LaserJet 1320
::   HP LaserJet 2015
::   HP LaserJet 2055
::   Brother MFC6400/8400/8600 series
::   For printing, all will use the
::   HP Universal Print Driver PCL5
:: ::::::::::::::::::::::::::::::::::::::::::::::::::::::


goto UENTER

:UENTER
COLOR 1F
cls

:: USER ENTERED VARIABLES
:: ::::::::::::::::::::::::::::::::::::::::::::::::::::::
:: The following section prompts the user for 
:: IP addresses and printer types.
:: ::::::::::::::::::::::::::::::::::::::::::::::::::::::

echo Please type the assigned IP Address (x.x.x.x) and Press ENTER [%IPAD%]
SET /P IPAD=
echo.
SET SUBN=255.255.255.240
echo Please type the assigned Subnet Mask or press ENTER [%SUBN%]
SET /P SUBN=
echo.
echo Please type the assigned Default Gateway (x.x.x.x) and Press Enter [%DFGW%]
SET /P DFGW=
echo.
echo Please type the assigned Primary DNS Server (x.x.x.x) and Press Enter [%DNS1%]
SET /P DNS1=
echo.
echo Please type the assigned Secondary DNS Server (x.x.x.x) and Press Enter [%DNS2%]
SET /P DNS2=
echo.
echo Please type the assigned Front Desk Printer IP Address (x.x.x.x) and Press Enter [%PRNT%]
SET /P PRNT=
:SETPRINTMOD
echo.
echo Please Select The Front Desk Printer Model From The Following:
echo ---------------------------------------------------------------
echo 1. HP LaserJet 2200 Series or Brother MFC8400/8600 Series [Network only]
echo 2. HP LaserJet 4000 Series
echo 3. HP LaserJet 4/5 Series
echo 4. HP LaserJet 1320 Series or HP LaserJet P2015 Series

echo.
echo N. None of the Above [You will install printer manually]
echo ---------------------------------------------------------------
SET /P PANSW=
if /I "%PANSW%" == "1" SET PMODEL=HP Universal Printing PCL 5
if /I "%PANSW%" == "1" goto SETBACKPRINT
if /I "%PANSW%" == "2" SET PMODEL=HP Universal Printing PCL 5
if /I "%PANSW%" == "2" goto SETBACKPRINT
if /I "%PANSW%" == "3" SET PMODEL=HP Universal Printing PCL 5
if /I "%PANSW%" == "3" goto SETBACKPRINT
if /I "%PANSW%" == "4" SET PMODEL=HP Universal Printing PCL 5
if /I "%PANSW%" == "4" goto SETBACKPRINT
if /I "%PANSW%" == "N" SET PMODEL=None of the Above
if /I "%PANSW%" == "N" goto SETBACKPRINT
echo.
echo !!!  ERROR  !!!
echo You must select either 1 2 3 4 or N
echo.
:: debug
goto SETPRINTMOD

:SETBACKPRINT
echo Do you have a Networked Back Office or GM's printer [ Y / N ]?
SET /P BPANSW=
if /I "%BPANSW%" == "N" goto VERIFICATION
:SETBACKPRINT2
echo Please Type The Assigned Back Office Printer IP Address (x.x.x.x) and Press Enter [%BPRNT%]
SET /P BPRNT=
echo.
echo Please Select The Back Office Printer Model
echo ----------------------------------------------------
echo 1. HP LaserJet 2200 Series or Brother MFC8400/8600 Series [Network only]
echo 2. HP LaserJet 4000 Series
echo 3. HP LaserJet 4/5 Series
echo 4. HP LaserJet 1320 Series or HP LaserJet P2015 Series
echo.
echo N. None of the Above [You will install printer manually]
echo ----------------------------------------------------
SET /P PANSW=
if /I "%PANSW%" == "1" SET BPMODEL=HP Universal Printing PCL 5
if /I "%PANSW%" == "1" goto VERIFICATION
if /I "%PANSW%" == "2" SET BPMODEL=HP Universal Printing PCL 5
if /I "%PANSW%" == "2" goto VERIFICATION
if /I "%PANSW%" == "3" SET BPMODEL=HP Universal Printing PCL 5
if /I "%PANSW%" == "3" goto VERIFICATION
if /I "%PANSW%" == "4" SET BPMODEL=HP Universal Printing PCL 5
if /I "%PANSW%" == "4" goto VERIFICATION
if /I "%PANSW%" == "N" SET BPMODEL=None of the Above
if /I "%PANSW%" == "N" goto VERIFICATION
echo.
echo !!!  ERROR  !!!
echo You must select either 1 2 3 4 or N
echo.
:: debug
goto SETBACKPRINT2

:VERIFICATION
:: This stuff ensures that all varaibles have a 
:: value assigned to them via keyboard input.
:: ::::::::::::::::::::::::::::::::::::::::::::::::::::::

COLOR 1F
cls
if /I "%SITE%" == "" (
goto ERRBLANK
) ELSE (
  if /I "%COMP%" == "" (
  goto ERRBLANK
  ) ELSE (
    if /I "%IPAD%" == "" (
    goto ERRBLANK
    ) ELSE (
      if /I "%PRNT%" == "" (
      goto ERRBLANK
      ) ELSE (
        if /I "%DFGW%" == "" (
        goto ERRBLANK
        ) ELSE (
          if /I "%DNS1%" == "" (
          goto ERRBLANK
          ) ELSE (
            if /I "%DNS2%" == "" (
            goto ERRBLANK
            )
          )
        )
      )
    )
  )
)
goto SKIPERRBLNK
:ERRBLANK

cls
echo.
echo !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
echo !!!                                                       !!!
echo !!!   You Cannot Continue - One or more lines are blank   !!!
echo !!!                                                       !!!
echo !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
echo.
echo All entries MUST be filled in...  
echo Returning to input section.
echo.
echo Press any key to continue... or Q to quit
SET /P ANSW=
if /I "%ANSW%" == "q" goto EXIT
SET ANSW=
goto UENTER
:SKIPERRBLNK


:: ::::::::::::::::::::::::::::::::::::::::::::::::::::
:: Status screen
:: Displays all input that will be passed to the
:: system if "y" is entered as a response to continue
:: ::::::::::::::::::::::::::::::::::::::::::::::::::::

echo -----------------------------------------------------
echo Please verify the information show below:
echo.  
echo -----------------------------------------------------
echo     !!!  VERIFY INFORMATION BELOW CAREFULLY  !!!
echo -----------------------------------------------------
echo.
echo Site ID: %SITE%       (Auto Generated off Computername)
echo Computer Type: %COMP%    (Auto Generated off Computername)
echo Computer Name: S%SITE%%COMP%
echo IP Address:      %IPAD%
echo Subnet Mask:     %SUBN%
echo Default Gateway: %DFGW%
echo Primary DNS:     %DNS1%
echo Secondary DNS:   %DNS2%
echo.  
echo Front Desk Printer IP Address: %PRNT%
echo Front Desk Printer Model: %PMODEL%
if /I "%BPANSW%" == "Y" echo -----------------------------------------------------
if /I "%BPANSW%" == "Y" echo Back Office Printer IP Address: %BPRNT%
if /I "%BPANSW%" == "Y" echo Back Office Printer Model: %BPMODEL%
echo -----------------------------------------------------
echo     !!!  VERIFY INFORMATION ABOVE CAREFULLY  !!!
echo -----------------------------------------------------
echo.
echo Are you sure this information is correct y/n or q to quit?

SET /P ANSW=
if /I "%ANSW%" == "y" goto BEGIN
if /I "%ANSW%" == "q" goto EXIT
goto UENTER



:BEGIN
COLOR 1F
echo.
echo ******************************************
echo.
:: ::::::::::::::::::::::::::::::::::::::::::::::::::::::
:: Sets IP address information including - 
:: IP address, Subnet Mask, Default Gateway
:: and Primary/Secondary DNS Server Addresses
:: ::::::::::::::::::::::::::::::::::::::::::::::::::::::

echo --- IP INFORMATION ---
echo Now Setting Network Interface IP Information:
echo IP Address:      %IPAD%
echo Subnet:          255.255.255.240
echo Default Gateway: %DFGW%
netsh interface ip set address name="Local Area Connection" source=static %IPAD% 255.255.255.240 %DFGW% 1
echo Setting DNS Servers:
echo Primary:   %DNS1%
netsh interface ip add dns name="Local Area Connection" %DNS1% index=1
echo Secondary: %DNS2%
netsh interface ip add dns name="Local Area Connection" %DNS2% index=2
echo.

netsh interface ip show config
echo.
echo IP Address Information Set ...

echo --- END IP INFORMATION ---
:: debug
color 1f
echo.

:: ::::::::::::::::::::::::::::::::::::::::::::::::::::::
:: This section will install the printers
:: The BackOffice printer will be installed
:: if it is specified earlier in the script
:: ::::::::::::::::::::::::::::::::::::::::::::::::::::::

echo --- FRONT DESK PRINTER INSTALLATION ---
:PRNTB
color 1f
echo Adding printer port
cscript %VBPATH%\prnport.vbs -a -r FrontDesk -h %PRNT% -o raw -n 9100
echo.
echo Adding printer
cscript %VBPATH%\prnmngr.vbs -a -p "FrontDesk" -m "%PMODEL%" -r "FrontDesk" 
echo.

echo --- END FRONT DESK PRINTER INSTALLATION ---
:: debug
color 1f
echo.

echo --- BACKOFFICE PRINTER INSTALLATION ---

if /I "%BPANSW%" == "N" goto PEGLINKS
color 1f
echo Adding Back Office printer port
cscript %VBPATH%\prnport.vbs -a -r BackOffice -h %BPRNT% -o raw -n 9100
echo.
echo Adding Back Office printer
cscript %VBPATH%\prnmngr.vbs -a -p "BackOffice" -m "%PMODEL%" -r "BackOffice" 
echo.

echo --- END BACKOFFICE PRINTER INSTALLATION ---

echo.
::  Creating NVBAK folder
call %progpath%MakNVBak.cmd
echo.
