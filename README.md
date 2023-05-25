# Time-Use-of-Youth-Cleaning-Data

*Cleaning data for Covid analysis - 2018 Quarter 1, 2018 September, 2019 quarter 1 and 3, 2020 quarter 1, 2020 September, 2021 Quarter 1 and 3, 2022 Quarter 1, 2022 September

*2018 QUARTER 1 - robustness check 
use "HOGT118.dta"
keep d_mes d_dia d_anio cd_a ent con v_sel n_hog h_mud
 
merge 1:m cd_a ent con v_sel n_hog h_mud using "SDEMT118.dta"

*New labels 
rename sex gender 
rename eda age
replace age = . if age == 99
rename nac_dia birthday
replace birthday = . if birthday == 99
rename nac_mes birthmonth
replace birthmonth = . if birthmonth == 99
rename nac_anio birthyear
replace birthyear = . if birthyear == 9999
rename cs_nr_ori stateeducation
rename eda19c agegroups
*education
rename cs_p13_1 degreecompleted
replace degreecompleted = . if degreecompleted == 9
rename cs_p13_2 yearscompleted 
label var yearscompleted "Years finished at schooling level"
rename cs_p16 finishedstudies
replace finishedstudies = . if finishedstudies == 9 
rename anios_esc  yearsofschool
rename cs_p12 readandwrite
rename cs_p17 attendedschool
*Work
rename hrsocup hoursperweek
rename ingocup  monthlyincome
rename ing_x_hrs incomeperhour
rename salario monthlysalary
rename ing7c incomelevels
rename p14apoyos supportprograms
rename clase3 employednopay
*family
rename n_hij children
replace children = . if children == 99
rename e_con marriagestatus
replace marriagestatus = . if marriagestatus == 9 
keep r_def cd_a ent con v_sel h_mud n_hog upm n_ren fac mun loc t_loc gender age birthday birthmonth degreecompleted stateeducation yearscompleted finishedstudies yearsofschool readandwrite attendedschool hoursperweek monthlyincome incomeperhour monthlysalary incomelevels supportprograms employednopay agegroups children marriagestatus d_dia d_mes d_anio 

save 2018_quarter1_DEMOGRAPHICS.dta, replace
clear

use "COE1T118.dta"
merge 1:1 cd_a ent con v_sel n_hog h_mud n_ren using "COE2T118.dta"

*identifiers
rename eda age
rename p1 workedlw
rename p1b hasjob
rename p4d1 jobsector
replace jobsector = . if jobsector == 9
rename p5c_thrs hoursworkedlw
replace hoursworkedlw = . if hoursworkedlw == 999
rename p5c_tdia daysworkedlw
replace daysworkedlw =. if daysworkedlw == 9
rename p5d averagehours
replace averagehours = . if averagehours== 9
rename p5e_thrs totalhours
replace totalhours = . if totalhours == 999
rename p5e_tdia totaldays
replace totaldays=. if totaldays == 9
rename ur urbanrural
rename p9f_anio lastyearworked
replace lastyearworked = . if lastyearworked == 9999
rename p9f_mes lastmonthworked
replace lastmonthworked = . if lastmonthworked == 99
rename p5e1 daysandhours 

*Other activities 
rename p11_1 studying 
rename p11_h1 hours_studying
rename p11_m1 minutes_studying 
rename p11_2 care_for_family 
rename p11_h2 hours_care 
rename p11_m2 minutes_care 
rename p11_3 home_purchases 
rename p11_h3 hours_purchases 
rename p11_m3 minutes_purchases 
rename p11_4 walk_family_toschool
rename p11_h4 hours_walktoschool
rename p11_m4 minutes_walktoschool
rename p11_5 home_construction
rename p11_h5 hours_construction
rename p11_m5 minutes_construction 
rename p11_6 home_repair 
rename p11_h6 hours_repair 
rename p11_m6 minutes_repair 
rename p11_7 homechores 
rename p11_h7 hours_chores
rename p11_m7 minutes_chores 
rename p11_8 community_service 
rename p11_h8 hours_communityservice
rename p11_m8 minutes_communityservice 

*looking for work
rename p2_1 foreignwork
rename p2_2 localwork
rename p2_3 selfemployed_withoutpay
rename p2_4 notsearching

rename p2a_dia firstsearchdate
replace firstsearchdate = . if firstsearchdate == 99
rename p2a_sem firstsearchweek
replace firstsearchweek = . if firstsearchweek == 9
rename p2a_mes firstsearchmonth
replace firstsearchmonth = . if firstsearchmonth == 99
rename p2a_anio firstsearchyear
replace firstsearchyear = . if firstsearchyear == 9999

rename p2b_dia lastsearchdate
replace lastsearchdate = . if lastsearchdate == 99
rename p2b_sem lastsearchweek
replace lastsearchweek = . if lastsearchweek == 9
rename p2b_mes lastsearchmonth
replace lastsearchmonth =. if lastsearchmonth == 99
rename p2b_anio lastsearchyear
replace lastsearchyear = . if lastsearchyear == 9999
rename p2g2 reasonnotsearching

*work
rename p2f needtowork
replace needtowork = . if needtowork == 9
rename p3j hascontract
replace hascontract = . if hascontract == 9
rename p3b selfemployed
rename p3h recievepay
rename p3l1 recievebonus
rename p3l2 paidvacation
rename p5f reason_noworklw
replace reason_noworklw = . if reason_noworklw == 99
rename p6d jobhealthbenefits
replace jobhealthbenefits=. if jobhealthbenefits == 9
rename p10_1 jobassistance 
replace jobassistance=0 if jobassistance==.
rename p10_2 microcredit
replace microcredit=0 if microcredit==.
rename p10_3 othergovprogram
replace othergovprogram=0 if othergovprogram==.
rename p10_4 nogovassistance
replace nogovassistance=0 if nogovassistance==.

keep v_sel fac age cd_a ent con h_mud r_def n_hog n_ren upm workedlw hasjob jobsector hoursworkedlw daysworkedlw averagehours totalhours daysandhours totaldays urbanrural lastyearworked lastmonthworked foreignwork localwork selfemployed notsearching firstsearchdate firstsearchweek firstsearchmonth firstsearchyear lastsearchdate lastsearchmonth lastsearchweek lastsearchyear reasonnotsearching needtowork hascontract selfemployed_withoutpay recievepay recievebonus paidvacation reason_noworklw jobhealthbenefits studying hours_studying minutes_studying care_for_family hours_care minutes_care home_purchases hours_purchases minutes_purchases walk_family_toschool hours_walktoschool minutes_walktoschool home_construction hours_construction minutes_construction home_repair hours_repair minutes_repair homechores hours_chores minutes_chores community_service hours_communityservice minutes_communityservice jobassistance microcredit othergovprogram nogovassistance

merge 1:1 cd_a ent con v_sel n_hog h_mud n_ren using "2018_quarter1_DEMOGRAPHICS.dta"

*2018 QUARTER 3 (SEPTEMBER) - robustness check
use "/HOGT318.dta"
keep d_mes d_dia d_anio cd_a ent con v_sel n_hog h_mud 

merge 1:m cd_a ent con v_sel n_hog h_mud using "SDEMT318.dta"

*New labels 
rename sex gender 
rename eda age
replace age = . if age == 99
rename nac_dia birthday
replace birthday = . if birthday == 99
rename nac_mes birthmonth
replace birthmonth = . if birthmonth == 99
rename nac_anio birthyear
replace birthyear = . if birthyear == 9999
rename cs_nr_ori stateeducation
rename eda19c agegroups
*education
rename cs_p13_1 degreecompleted
replace degreecompleted = . if degreecompleted == 9
rename cs_p13_2 yearscompleted 
label var yearscompleted "Years finished at schooling level"
rename cs_p16 finishedstudies
replace finishedstudies = . if finishedstudies == 9 
rename anios_esc  yearsofschool
rename cs_p12 readandwrite
rename cs_p17 attendedschool
*Work
rename hrsocup hoursperweek
rename ingocup  monthlyincome
rename ing_x_hrs incomeperhour
rename salario monthlysalary
rename ing7c incomelevels
rename p14apoyos supportprograms
rename clase3 employednopay
*family
rename n_hij children
replace children = . if children == 99
rename e_con marriagestatus
replace marriagestatus = . if marriagestatus == 9 
keep r_def cd_a ent con v_sel h_mud n_hog upm n_ren fac mun loc t_loc gender age birthday birthmonth degreecompleted stateeducation yearscompleted finishedstudies yearsofschool readandwrite attendedschool hoursperweek monthlyincome incomeperhour monthlysalary incomelevels supportprograms employednopay agegroups children marriagestatus d_dia d_mes d_anio 

save 2018_quarter3_DEMOGRAPHICS.dta, replace
clear 

use "COE1T318.dta"
merge 1:1 cd_a ent con v_sel n_hog h_mud n_ren using "COE2T318.dta"

rename eda age
rename p1 workedlw
rename p1b hasjob
rename p4d1 jobsector
replace jobsector = . if jobsector == 9
rename p5b_thrs hoursworkedlw
replace hoursworkedlw = . if hoursworkedlw == 999
rename p5b_tdia daysworkedlw
replace daysworkedlw =. if daysworkedlw == 9
rename p5c averagehours
replace averagehours = . if averagehours== 9
rename p5d_thrs totalhours
replace totalhours = . if totalhours == 999
rename p5d_tdia totaldays
replace totaldays=. if totaldays == 9
rename ur urbanrural
rename p2k_anio lastyearworked
replace lastyearworked = . if lastyearworked == 9999
rename p2k_mes lastmonthworked
replace lastmonthworked = . if lastmonthworked == 99
rename p5d1 daysandhours 

*Other activities 
rename p9_1 studying 
rename p9_h1 hours_studying
rename p9_m1 minutes_studying 
rename p9_2 care_for_family 
rename p9_h2 hours_care 
rename p9_m2 minutes_care 
rename p9_3 home_purchases 
rename p9_h3 hours_purchases 
rename p9_m3 minutes_purchases 
rename p9_4 walk_family_toschool
rename p9_h4 hours_walktoschool
rename p9_m4 minutes_walktoschool
rename p9_5 home_construction
rename p9_h5 hours_construction
rename p9_m5 minutes_construction 
rename p9_6 home_repair 
rename p9_h6 hours_repair 
rename p9_m6 minutes_repair 
rename p9_7 homechores 
rename p9_h7 hours_chores
rename p9_m7 minutes_chores 
rename p9_8 community_service 
rename p9_h8 hours_communityservice
rename p9_m8 minutes_communityservice 

*looking for work
rename p2_1 foreignwork
rename p2_2 localwork
rename p2_3 selfemployed_withoutpay
rename p2_4 notsearching
rename p2a_dia firstsearchdate
replace firstsearchdate = . if firstsearchdate == 99
rename p2a_sem firstsearchweek
replace firstsearchweek = . if firstsearchweek == 9
rename p2a_mes firstsearchmonth
replace firstsearchmonth = . if firstsearchmonth == 99
rename p2a_anio firstsearchyear
replace firstsearchyear = . if firstsearchyear == 9999
rename p2b_dia lastsearchdate
replace lastsearchdate = . if lastsearchdate == 99
rename p2b_sem lastsearchweek
replace lastsearchweek = . if lastsearchweek == 9
rename p2b_mes lastsearchmonth
replace lastsearchmonth =. if lastsearchmonth == 99
rename p2b_anio lastsearchyear
replace lastsearchyear = . if lastsearchyear == 9999
rename p2g2 reasonnotsearching

*work
rename p2f needtowork
replace needtowork = . if needtowork == 9
rename p3i hascontract
replace hascontract = . if hascontract == 9
rename p3b selfemployed
rename p3h recievepay
rename p3k1 recievebonus
rename p3k2 paidvacation
rename p5e reason_noworklw
replace reason_noworklw = . if reason_noworklw == 99
rename p6d jobhealthbenefits
replace jobhealthbenefits=. if jobhealthbenefits == 9
keep v_sel fac age cd_a ent con h_mud r_def n_hog n_ren upm workedlw hasjob jobsector hoursworkedlw daysworkedlw averagehours totalhours daysandhours totaldays urbanrural lastyearworked lastmonthworked foreignwork localwork selfemployed notsearching firstsearchdate firstsearchweek firstsearchmonth firstsearchyear lastsearchdate lastsearchmonth lastsearchweek lastsearchyear reasonnotsearching needtowork hascontract selfemployed_withoutpay recievepay recievebonus paidvacation reason_noworklw jobhealthbenefits studying hours_studying minutes_studying care_for_family hours_care minutes_care home_purchases hours_purchases minutes_purchases walk_family_toschool hours_walktoschool minutes_walktoschool home_construction hours_construction minutes_construction home_repair hours_repair minutes_repair homechores hours_chores minutes_chores community_service hours_communityservice minutes_communityservice 

merge 1:1 cd_a ent con v_sel n_hog h_mud n_ren using "2018_quarter3_DEMOGRAPHICS.dta"
save "2018_quarter3.dta", replace 


*2019 QUARTER 1
use "hogt119.dta"
keep D_MES D_DIA D_ANIO CD_A ENT CON V_SEL N_HOG H_MUD

merge 1:m CD_A ENT CON V_SEL N_HOG H_MUD using "sdemt119.dta"

rename D_MES d_mes
rename D_DIA d_dia 
rename D_ANIO d_anio
rename UPM upm
rename CON con
rename R_DEF r_def
rename CD_A cd_a
rename ENT ent
rename N_HOG n_hog
rename H_MUD h_mud
rename N_REN n_ren
rename V_SEL v_sel
rename MUN mun
rename FAC fac

rename SEX gender 
rename LOC loc
rename T_LOC t_loc
rename EDA age 
rename NAC_DIA birthday
destring birthday, replace 
replace birthday = . if birthday == 99
rename NAC_MES birthmonth
destring birthmonth, replace 
replace birthmonth = . if birthmonth == 99
rename NAC_ANIO birthyear
destring birthyear, replace 
replace birthyear = . if birthyear == 9999
rename CS_NR_ORI stateeducation
rename EDA19C agegroups
*education
rename CS_P13_1 degreecompleted
replace degreecompleted = . if degreecompleted == 9
rename CS_P13_2 yearscompleted 
label var yearscompleted "Years finished at schooling level"
rename CS_P16 finishedstudies
replace finishedstudies = . if finishedstudies == 9 
rename ANIOS_ESC yearsofschool
rename CS_P12 readandwrite
rename CS_P17 attendedschool
*Work
rename HRSOCUP hoursperweek
rename INGOCUP monthlyincome
rename ING_X_HRS incomeperhour
rename SALARIO monthlysalary
rename ING7C incomelevels
rename P14APOYOS supportprograms
rename CLASE3 employednopay
*family
rename N_HIJ children
replace children = . if children == 99
rename E_CON marriagestatus
replace marriagestatus = . if marriagestatus == 9 
keep r_def cd_a ent con v_sel h_mud n_hog upm n_ren fac mun loc t_loc gender age birthday birthmonth degreecompleted stateeducation yearscompleted finishedstudies yearsofschool readandwrite attendedschool hoursperweek monthlyincome incomeperhour monthlysalary incomelevels supportprograms employednopay agegroups children marriagestatus d_dia d_mes d_anio 

save 2019_quarter1_DEMOGRAPHICS.dta, replace
clear

use "coe1t119.dta"

rename R_DEF r_def 
rename CD_A cd_a
rename D_SEM d_sem
rename V_SEL v_sel
rename N_HOG n_hog
rename H_MUD h_mud
rename N_ENT n_ent
rename N_REN n_ren
rename ENT ent 
rename CON con 
rename UPM upm
rename PER per
rename N_PRO_VIV n_pro_viv
rename FAC fac
merge 1:1 cd_a ent con n_hog h_mud n_ren v_sel using "coe2t119.dta"

*identifiers
rename EDA age
rename P1 workedlw
rename P1B hasjob
rename P4D1 jobsector
replace jobsector = . if jobsector == 9
rename P5C_THRS hoursworkedlw
replace hoursworkedlw = . if hoursworkedlw == 999
rename P5C_TDIA daysworkedlw
replace daysworkedlw =. if daysworkedlw == 9
rename P5D averagehours
replace averagehours = . if averagehours== 9
rename P5E_THRS totalhours
replace totalhours = . if totalhours == 999
rename P5E_TDIA totaldays
replace totaldays=. if totaldays == 9
rename UR urbanrural
rename p9f_anio lastyearworked
replace lastyearworked = . if lastyearworked == 9999
rename p9f_mes lastmonthworked
replace lastmonthworked = . if lastmonthworked == 99
rename P5E1 daysandhours 

*Other activities 
rename p11_1 studying 
rename p11_h1 hours_studying
rename p11_m1 minutes_studying 
rename p11_2 care_for_family 
rename p11_h2 hours_care 
rename p11_m2 minutes_care 
rename p11_3 home_purchases 
rename p11_h3 hours_purchases 
rename p11_m3 minutes_purchases 
rename p11_4 walk_family_toschool
rename p11_h4 hours_walktoschool
rename p11_m4 minutes_walktoschool
rename p11_5 home_construction
rename p11_h5 hours_construction
rename p11_m5 minutes_construction 
rename p11_6 home_repair 
rename p11_h6 hours_repair 
rename p11_m6 minutes_repair 
rename p11_7 homechores 
rename p11_h7 hours_chores
rename p11_m7 minutes_chores 
rename p11_8 community_service 
rename p11_h8 hours_communityservice
rename p11_m8 minutes_communityservice 

*looking for work
rename P2_1 foreignwork
rename P2_2 localwork
rename P2_3 selfemployed_withoutpay
rename P2_4 notsearching

rename P2A_DIA firstsearchdate
replace firstsearchdate = . if firstsearchdate == 99
rename P2A_SEM firstsearchweek
replace firstsearchweek = . if firstsearchweek == 9
rename P2A_MES firstsearchmonth
replace firstsearchmonth = . if firstsearchmonth == 99
rename P2A_ANIO firstsearchyear
replace firstsearchyear = . if firstsearchyear == 9999

rename P2B_DIA lastsearchdate
replace lastsearchdate = . if lastsearchdate == 99
rename P2B_SEM lastsearchweek
replace lastsearchweek = . if lastsearchweek == 9
rename P2B_MES lastsearchmonth
replace lastsearchmonth =. if lastsearchmonth == 99
rename P2B_ANIO lastsearchyear
replace lastsearchyear = . if lastsearchyear == 9999
rename P2G2 reasonnotsearching

*work
rename P2F needtowork
replace needtowork = . if needtowork == 9
rename P3J hascontract
replace hascontract = . if hascontract == 9
rename P3B selfemployed
rename P3H recievepay
rename P3L1 recievebonus
rename P3L2 paidvacation
rename P5F reason_noworklw
replace reason_noworklw = . if reason_noworklw == 99
rename p6d jobhealthbenefits
replace jobhealthbenefits=. if jobhealthbenefits == 9
rename p10_1 jobassistance 
replace jobassistance=0 if jobassistance==.
rename p10_2 microcredit
replace microcredit=0 if microcredit==.
rename p10_3 othergovprogram
replace othergovprogram=0 if othergovprogram==.
rename p10_4 nogovassistance
replace nogovassistance=0 if nogovassistance==.

keep v_sel fac age cd_a ent con h_mud r_def n_hog n_ren upm workedlw hasjob jobsector hoursworkedlw daysworkedlw averagehours totalhours daysandhours totaldays urbanrural lastyearworked lastmonthworked foreignwork localwork selfemployed notsearching firstsearchdate firstsearchweek firstsearchmonth firstsearchyear lastsearchdate lastsearchmonth lastsearchweek lastsearchyear reasonnotsearching needtowork hascontract selfemployed_withoutpay recievepay recievebonus paidvacation reason_noworklw jobhealthbenefits studying hours_studying minutes_studying care_for_family hours_care minutes_care home_purchases hours_purchases minutes_purchases walk_family_toschool hours_walktoschool minutes_walktoschool home_construction hours_construction minutes_construction home_repair hours_repair minutes_repair homechores hours_chores minutes_chores community_service hours_communityservice minutes_communityservice jobassistance microcredit othergovprogram nogovassistance

merge 1:1 cd_a ent con v_sel n_hog h_mud n_ren using "2019_quarter1_DEMOGRAPHICS.dta"

save 2019_quarter1.dta, replace 


*2019 QUARTER 3//September
use "HOGT319.dta"

keep d_mes d_dia d_anio cd_a ent con v_sel n_hog h_mud 
merge 1:m cd_a ent con v_sel n_hog h_mud using "SDEMT319.dta"

*New labels 
rename sex gender 
rename eda age
replace age = . if age == 99
rename nac_dia birthday
replace birthday = . if birthday == 99
rename nac_mes birthmonth
replace birthmonth = . if birthmonth == 99
rename nac_anio birthyear
replace birthyear = . if birthyear == 9999
rename cs_nr_ori stateeducation
rename eda19c agegroups
*education
rename cs_p13_1 degreecompleted
replace degreecompleted = . if degreecompleted == 9
rename cs_p13_2 yearscompleted 
label var yearscompleted "Years finished at schooling level"
rename cs_p16 finishedstudies
replace finishedstudies = . if finishedstudies == 9 
rename anios_esc  yearsofschool
rename cs_p12 readandwrite
rename cs_p17 attendedschool
*Work
rename hrsocup hoursperweek
rename ingocup  monthlyincome
rename ing_x_hrs incomeperhour
rename salario monthlysalary
rename clase1 economicallyactive
rename ing7c incomelevels
rename medica5c healthbenefits
rename p14apoyos supportprograms
rename zona salaryzone
rename clase3 employednopay
rename seg_soc institutionaccess
*family
rename n_hij children
replace children = . if children == 99
rename e_con marriagestatus
replace marriagestatus = . if marriagestatus == 9 

keep r_def cd_a ent con v_sel h_mud n_hog upm n_ren fac mun loc t_loc gender age birthday birthmonth degreecompleted stateeducation yearscompleted finishedstudies yearsofschool readandwrite attendedschool hoursperweek monthlyincome incomeperhour monthlysalary economicallyactive incomelevels healthbenefits supportprograms salaryzone employednopay institutionaccess agegroups children marriagestatus d_mes d_dia d_anio

save 2019_quarter3_demographics.dta, replace 
clear 

use "COE1T319.dta"
merge 1:1 cd_a ent con v_sel n_hog h_mud n_ren using "COE2T319.dta"

*identifiers
rename eda age
rename p1 workedlw
rename p1b hasjob
rename p4d1 jobsector
replace jobsector = . if jobsector == 9
rename p5b_thrs hoursworkedlw
replace hoursworkedlw = . if hoursworkedlw == 999
rename p5b_tdia daysworkedlw
replace daysworkedlw =. if daysworkedlw == 9
rename p5c averagehours
replace averagehours = . if averagehours== 9
rename p5d_thrs totalhours
replace totalhours = . if totalhours == 999
rename p5d_tdia totaldays
replace totaldays=. if totaldays == 9
rename ur urbanrural
rename p2k_anio lastyearworked
replace lastyearworked = . if lastyearworked == 9999
rename p2k_mes lastmonthworked
replace lastmonthworked = . if lastmonthworked == 99
rename p5d1 daysandhours 

*Other activities 
rename p9_1 studying 
rename p9_h1 hours_studying
rename p9_m1 minutes_studying 
rename p9_2 care_for_family 
rename p9_h2 hours_care 
rename p9_m2 minutes_care 
rename p9_3 home_purchases 
rename p9_h3 hours_purchases 
rename p9_m3 minutes_purchases 
rename p9_4 walk_family_toschool
rename p9_h4 hours_walktoschool
rename p9_m4 minutes_walktoschool
rename p9_5 home_construction
rename p9_h5 hours_construction
rename p9_m5 minutes_construction 
rename p9_6 home_repair 
rename p9_h6 hours_repair 
rename p9_m6 minutes_repair 
rename p9_7 homechores 
rename p9_h7 hours_chores
rename p9_m7 minutes_chores 
rename p9_8 community_service 
rename p9_h8 hours_communityservice
rename p9_m8 minutes_communityservice 

*looking for work
rename p2_1 foreignwork
rename p2_2 localwork
rename p2_3 selfemployed_withoutpay
rename p2_4 notsearching
rename p2a_dia firstsearchdate
replace firstsearchdate = . if firstsearchdate == 99
rename p2a_sem firstsearchweek
replace firstsearchweek = . if firstsearchweek == 9
rename p2a_mes firstsearchmonth
replace firstsearchmonth = . if firstsearchmonth == 99
rename p2a_anio firstsearchyear
replace firstsearchyear = . if firstsearchyear == 9999
rename p2b_dia lastsearchdate
replace lastsearchdate = . if lastsearchdate == 99
rename p2b_sem lastsearchweek
replace lastsearchweek = . if lastsearchweek == 9
rename p2b_mes lastsearchmonth
replace lastsearchmonth =. if lastsearchmonth == 99
rename p2b_anio lastsearchyear
replace lastsearchyear = . if lastsearchyear == 9999
rename p2g2 reasonnotsearching

*work
rename p2f needtowork
replace needtowork = . if needtowork == 9
rename p3i hascontract
replace hascontract = . if hascontract == 9
rename p3b selfemployed
rename p3h recievepay
rename p3k1 recievebonus
rename p3k2 paidvacation
rename p5e reason_noworklw
replace reason_noworklw = . if reason_noworklw == 99
rename p6d jobhealthbenefits
replace jobhealthbenefits=. if jobhealthbenefits == 9

keep v_sel fac age cd_a ent con h_mud r_def n_hog n_ren upm workedlw hasjob jobsector hoursworkedlw daysworkedlw averagehours totalhours daysandhours totaldays urbanrural lastyearworked lastmonthworked foreignwork localwork selfemployed notsearching firstsearchdate firstsearchweek firstsearchmonth firstsearchyear lastsearchdate lastsearchmonth lastsearchweek lastsearchyear reasonnotsearching needtowork hascontract selfemployed_withoutpay recievepay recievebonus paidvacation reason_noworklw jobhealthbenefits studying hours_studying minutes_studying care_for_family hours_care minutes_care home_purchases hours_purchases minutes_purchases walk_family_toschool hours_walktoschool minutes_walktoschool home_construction hours_construction minutes_construction home_repair hours_repair minutes_repair homechores hours_chores minutes_chores community_service hours_communityservice minutes_communityservice 

merge 1:1 cd_a ent con v_sel n_hog h_mud n_ren using "2019_quarter3_demographics.dta"
save 2019_quarter3.dta, replace 


*2020 QUARTER 1
use "HOGT120.dta"

keep d_mes d_dia d_anio cd_a ent con v_sel n_hog h_mud 

merge 1:m cd_a ent con v_sel n_hog h_mud using "SDEMT120.dta"
*New labels 
rename sex gender 
rename eda age
replace age = . if age == 99
rename nac_dia birthday
replace birthday = . if birthday == 99
rename nac_mes birthmonth
replace birthmonth = . if birthmonth == 99
rename nac_anio birthyear
replace birthyear = . if birthyear == 9999
rename cs_nr_ori stateeducation
rename eda19c agegroups
*education
rename cs_p13_1 degreecompleted
replace degreecompleted = . if degreecompleted == 9
rename cs_p13_2 yearscompleted 
label var yearscompleted "Years finished at schooling level"
rename cs_p16 finishedstudies
replace finishedstudies = . if finishedstudies == 9 
rename anios_esc  yearsofschool
rename cs_p12 readandwrite
rename cs_p17 attendedschool
*Work
rename hrsocup hoursperweek
rename ingocup  monthlyincome
rename ing_x_hrs incomeperhour
rename salario monthlysalary
rename clase1 economicallyactive
rename ing7c incomelevels
rename medica5c healthbenefits
rename p14apoyos supportprograms
rename zona salaryzone
rename clase3 employednopay
rename seg_soc institutionaccess


*family
rename n_hij children
replace children = . if children == 99
rename e_con marriagestatus
replace marriagestatus = . if marriagestatus == 9 

keep r_def cd_a ent con v_sel h_mud n_hog upm n_ren fac mun loc t_loc gender age birthday birthmonth degreecompleted stateeducation yearscompleted finishedstudies yearsofschool readandwrite attendedschool hoursperweek monthlyincome incomeperhour monthlysalary economicallyactive incomelevels healthbenefits supportprograms salaryzone employednopay institutionaccess agegroups children marriagestatus d_mes d_dia d_anio

save 2020_quarter1_demographics.dta, replace 

use "COE1T120.dta"
merge 1:1 con ent cd_a n_hog h_mud n_ren v_sel using "COE2T120.dta"

*identifiers
rename eda age
rename p1 workedlw
rename p1b hasjob
rename p4d1 jobsector
replace jobsector = . if jobsector == 9
rename p5c_thrs hoursworkedlw
replace hoursworkedlw = . if hoursworkedlw == 999
rename p5c_tdia daysworkedlw
replace daysworkedlw =. if daysworkedlw == 9
rename p5d averagehours
replace averagehours = . if averagehours== 9
rename p5e_thrs totalhours
replace totalhours = . if totalhours == 999
rename p5e_tdia totaldays
replace totaldays=. if totaldays == 9
rename ur urbanrural
rename p9f_anio lastyearworked
replace lastyearworked = . if lastyearworked == 9999
rename p9f_mes lastmonthworked
replace lastmonthworked = . if lastmonthworked == 99
rename p5e1 daysandhours 

*Other activities 
rename p11_1 studying 
rename p11_h1 hours_studying
rename p11_m1 minutes_studying 
rename p11_2 care_for_family 
rename p11_h2 hours_care 
rename p11_m2 minutes_care 
rename p11_3 home_purchases 
rename p11_h3 hours_purchases 
rename p11_m3 minutes_purchases 
rename p11_4 walk_family_toschool
rename p11_h4 hours_walktoschool
rename p11_m4 minutes_walktoschool
rename p11_5 home_construction
rename p11_h5 hours_construction
rename p11_m5 minutes_construction 
rename p11_6 home_repair 
rename p11_h6 hours_repair 
rename p11_m6 minutes_repair 
rename p11_7 homechores 
rename p11_h7 hours_chores
rename p11_m7 minutes_chores 
rename p11_8 community_service 
rename p11_h8 hours_communityservice
rename p11_m8 minutes_communityservice 

*looking for work
rename p2_1 foreignwork
rename p2_2 localwork
rename p2_3 selfemployed_withoutpay
rename p2_4 notsearching

rename p2a_dia firstsearchdate
replace firstsearchdate = . if firstsearchdate == 99
rename p2a_sem firstsearchweek
replace firstsearchweek = . if firstsearchweek == 9
rename p2a_mes firstsearchmonth
replace firstsearchmonth = . if firstsearchmonth == 99
rename p2a_anio firstsearchyear
replace firstsearchyear = . if firstsearchyear == 9999

rename p2b_dia lastsearchdate
replace lastsearchdate = . if lastsearchdate == 99
rename p2b_sem lastsearchweek
replace lastsearchweek = . if lastsearchweek == 9
rename p2b_mes lastsearchmonth
replace lastsearchmonth =. if lastsearchmonth == 99
rename p2b_anio lastsearchyear
replace lastsearchyear = . if lastsearchyear == 9999
rename p2g2 reasonnotsearching

*work
rename p2f needtowork
replace needtowork = . if needtowork == 9
rename p3j hascontract
replace hascontract = . if hascontract == 9
rename p3b selfemployed
rename p3h recievepay
rename p3l1 recievebonus
rename p3l2 paidvacation
rename p5f reason_noworklw
replace reason_noworklw = . if reason_noworklw == 99
rename p6d jobhealthbenefits
replace jobhealthbenefits=. if jobhealthbenefits == 9
rename p10_1 jobassistance 
replace jobassistance=0 if jobassistance==.
rename p10_2 microcredit
replace microcredit=0 if microcredit==.
rename p10_3 othergovprogram
replace othergovprogram=0 if othergovprogram==.
rename p10_4 nogovassistance
replace nogovassistance=0 if nogovassistance==.

keep v_sel fac age cd_a ent con h_mud r_def n_hog n_ren upm workedlw hasjob jobsector hoursworkedlw daysworkedlw averagehours totalhours daysandhours totaldays urbanrural lastyearworked lastmonthworked foreignwork localwork selfemployed notsearching firstsearchdate firstsearchweek firstsearchmonth firstsearchyear lastsearchdate lastsearchmonth lastsearchweek lastsearchyear reasonnotsearching needtowork hascontract selfemployed_withoutpay recievepay recievebonus paidvacation reason_noworklw jobhealthbenefits studying hours_studying minutes_studying care_for_family hours_care minutes_care home_purchases hours_purchases minutes_purchases walk_family_toschool hours_walktoschool minutes_walktoschool home_construction hours_construction minutes_construction home_repair hours_repair minutes_repair homechores hours_chores minutes_chores community_service hours_communityservice minutes_communityservice jobassistance microcredit othergovprogram nogovassistance

merge 1:1 cd_a ent con v_sel n_hog h_mud n_ren using "2020_quarter1_demographics.dta"


save 2020_quarter1.dta, replace 


*2020 QUARTER 3//SEPTEMBER

use "enoen_hogt320.dta"

keep d_dia d_mes d_anio cd_a ent con v_sel tipo mes_cal ca n_hog h_mud 

merge 1:m v_sel n_hog h_mud cd_a ent con tipo mes_cal ca using "enoen_sdemt320.dta"

*New labels 
rename sex gender 
rename eda age
replace age = . if age == 99
rename nac_dia birthday
replace birthday = . if birthday == 99
rename nac_mes birthmonth
replace birthmonth = . if birthmonth == 99
rename nac_anio birthyear
replace birthyear = . if birthyear == 9999
rename cs_nr_ori stateeducation
rename eda19c agegroups
*education
rename cs_p13_1 degreecompleted
replace degreecompleted = . if degreecompleted == 9
rename cs_p13_2 yearscompleted 
label var yearscompleted "Years finished at schooling level"
rename cs_p16 finishedstudies
replace finishedstudies = . if finishedstudies == 9 
rename anios_esc  yearsofschool
rename cs_p12 readandwrite
rename cs_p17 attendedschool
*Work
rename hrsocup hoursperweek
rename ingocup  monthlyincome
rename ing_x_hrs incomeperhour
rename salario monthlysalary
rename ing7c incomelevels
rename p14apoyos supportprograms
rename clase3 employednopay
*family
rename n_hij children
replace children = . if children == 99
rename e_con marriagestatus
replace marriagestatus = . if marriagestatus == 9 
keep r_def cd_a ent con v_sel h_mud n_hog tipo mes_cal ca upm n_ren fac_tri fac_men mun loc t_loc_tri t_loc_men gender age birthday birthmonth degreecompleted stateeducation yearscompleted finishedstudies yearsofschool readandwrite attendedschool hoursperweek monthlyincome incomeperhour monthlysalary incomelevels supportprograms employednopay agegroups children marriagestatus d_dia d_mes d_anio 

save 2020_Q3_DEMOGRAPHICS.dta, replace 

use "enoen_coe1t320.dta"

merge 1:1 v_sel n_hog h_mud cd_a ent con tipo mes_cal ca  n_ren using "enoen_coe2t320.dta"

rename eda age
rename p1 workedlw
rename p1b hasjob
rename p4d1 jobsector
replace jobsector = . if jobsector == 9
rename p5b_thrs hoursworkedlw
replace hoursworkedlw = . if hoursworkedlw == 999
rename p5b_tdia daysworkedlw
replace daysworkedlw =. if daysworkedlw == 9
rename p5c averagehours
replace averagehours = . if averagehours== 9
rename p5d_thrs totalhours
replace totalhours = . if totalhours == 999
rename p5d_tdia totaldays
replace totaldays=. if totaldays == 9
rename ur urbanrural
rename p2k_anio lastyearworked
replace lastyearworked = . if lastyearworked == 9999
rename p2k_mes lastmonthworked
replace lastmonthworked = . if lastmonthworked == 99
rename p5d1 daysandhours 

*Other activities 
rename p9_1 studying 
rename p9_h1 hours_studying
rename p9_m1 minutes_studying 
rename p9_2 care_for_family 
rename p9_h2 hours_care 
rename p9_m2 minutes_care 
rename p9_3 home_purchases 
rename p9_h3 hours_purchases 
rename p9_m3 minutes_purchases 
rename p9_4 walk_family_toschool
rename p9_h4 hours_walktoschool
rename p9_m4 minutes_walktoschool
rename p9_5 home_construction
rename p9_h5 hours_construction
rename p9_m5 minutes_construction 
rename p9_6 home_repair 
rename p9_h6 hours_repair 
rename p9_m6 minutes_repair 
rename p9_7 homechores 
rename p9_h7 hours_chores
rename p9_m7 minutes_chores 
rename p9_8 community_service 
rename p9_h8 hours_communityservice
rename p9_m8 minutes_communityservice 

*looking for work
rename p2_1 foreignwork
rename p2_2 localwork
rename p2_3 selfemployed_withoutpay
rename p2_4 notsearching
rename p2a_dia firstsearchdate
replace firstsearchdate = . if firstsearchdate == 99
rename p2a_sem firstsearchweek
replace firstsearchweek = . if firstsearchweek == 9
rename p2a_mes firstsearchmonth
replace firstsearchmonth = . if firstsearchmonth == 99
rename p2a_anio	firstsearchyear
replace firstsearchyear = . if firstsearchyear == 9999
rename p2b_dia lastsearchdate
replace lastsearchdate = . if lastsearchdate == 99
rename p2b_sem lastsearchweek
replace lastsearchweek = . if lastsearchweek == 9
rename p2b_mes lastsearchmonth
replace lastsearchmonth =. if lastsearchmonth == 99
rename p2b_anio lastsearchyear
replace lastsearchyear = . if lastsearchyear == 9999
rename p2g2 reasonnotsearching

*work
rename p2f needtowork
replace needtowork = . if needtowork == 9
rename p3i hascontract
replace hascontract = . if hascontract == 9
rename p3b selfemployed
rename p3h recievepay
rename p3k1 recievebonus
rename p3k2 paidvacation
rename p5e reason_noworklw
replace reason_noworklw = . if reason_noworklw == 99
rename p6d jobhealthbenefits
replace jobhealthbenefits=. if jobhealthbenefits == 9
keep v_sel fac_tri fac_men age cd_a ent con h_mud r_def n_hog n_ren tipo mes_cal ca upm workedlw hasjob jobsector hoursworkedlw daysworkedlw averagehours totalhours daysandhours totaldays urbanrural lastyearworked lastmonthworked foreignwork localwork selfemployed notsearching firstsearchdate firstsearchweek firstsearchmonth firstsearchyear lastsearchdate lastsearchmonth lastsearchweek lastsearchyear reasonnotsearching needtowork hascontract selfemployed_withoutpay recievepay recievebonus paidvacation reason_noworklw jobhealthbenefits studying hours_studying minutes_studying care_for_family hours_care minutes_care home_purchases hours_purchases minutes_purchases walk_family_toschool hours_walktoschool minutes_walktoschool home_construction hours_construction minutes_construction home_repair hours_repair minutes_repair homechores hours_chores minutes_chores community_service hours_communityservice minutes_communityservice 

merge 1:1 v_sel n_hog h_mud cd_a ent con tipo mes_cal ca  n_ren using "2020_Q3_DEMOGRAPHICS.dta"

save 2020_Q3.dta, replace

*2021 QUARTER 1
use "/HOGT121.dta"
keep d_mes d_dia d_anio cd_a ent con v_sel n_hog h_mud 

merge 1:m cd_a ent con v_sel n_hog h_mud using "SDEMT121.dta"

*New labels 
rename sex gender 
rename eda age
replace age = . if age == 99
rename nac_dia birthday
replace birthday = . if birthday == 99
rename nac_mes birthmonth
replace birthmonth = . if birthmonth == 99
rename nac_anio birthyear
replace birthyear = . if birthyear == 9999
rename cs_nr_ori stateeducation
rename eda19c agegroups
*education
rename cs_p13_1 degreecompleted
replace degreecompleted = . if degreecompleted == 9
rename cs_p13_2 yearscompleted 
label var yearscompleted "Years finished at schooling level"
rename cs_p16 finishedstudies
replace finishedstudies = . if finishedstudies == 9 
rename anios_esc  yearsofschool
rename cs_p12 readandwrite
rename cs_p17 attendedschool
*Work
rename hrsocup hoursperweek
rename ingocup  monthlyincome
rename ing_x_hrs incomeperhour
rename salario monthlysalary
rename ing7c incomelevels
rename p14apoyos supportprograms
rename clase3 employednopay
*family
rename n_hij children
replace children = . if children == 99
rename e_con marriagestatus
replace marriagestatus = . if marriagestatus == 9 
keep r_def cd_a ent con v_sel h_mud n_hog upm n_ren fac mun loc t_loc gender age birthday birthmonth degreecompleted stateeducation yearscompleted finishedstudies yearsofschool readandwrite attendedschool hoursperweek monthlyincome incomeperhour monthlysalary incomelevels supportprograms employednopay agegroups children marriagestatus d_dia d_mes d_anio 

save 2021_Q1_DEMOGRAPHICS.dta, replace
clear 

use "COE1T121.dta"
merge 1:1 cd_a ent con v_sel n_hog h_mud n_ren using "COE2T121.dta"

rename eda age
rename p1 workedlw
rename p1b hasjob
rename p4d1 jobsector
replace jobsector = . if jobsector == 9
rename p5b_thrs hoursworkedlw
replace hoursworkedlw = . if hoursworkedlw == 999
rename p5b_tdia daysworkedlw
replace daysworkedlw =. if daysworkedlw == 9
rename p5c averagehours
replace averagehours = . if averagehours== 9
rename p5d_thrs totalhours
replace totalhours = . if totalhours == 999
rename p5d_tdia totaldays
replace totaldays=. if totaldays == 9
rename ur urbanrural
rename p2k_anio lastyearworked
replace lastyearworked = . if lastyearworked == 9999
rename p2k_mes lastmonthworked
replace lastmonthworked = . if lastmonthworked == 99
rename p5d1 daysandhours 

*Other activities 
rename p11_1 studying 
rename p11_h1 hours_studying
rename p11_m1 minutes_studying 
rename p11_2 care_for_family 
rename p11_h2 hours_care 
rename p11_m2 minutes_care 
rename p11_3 home_purchases 
rename p11_h3 hours_purchases 
rename p11_m3 minutes_purchases 
rename p11_4 walk_family_toschool
rename p11_h4 hours_walktoschool
rename p11_m4 minutes_walktoschool
rename p11_5 home_construction
rename p11_h5 hours_construction
rename p11_m5 minutes_construction 
rename p11_6 home_repair 
rename p11_h6 hours_repair 
rename p11_m6 minutes_repair 
rename p11_7 homechores 
rename p11_h7 hours_chores
rename p11_m7 minutes_chores 
rename p11_8 community_service 
rename p11_h8 hours_communityservice
rename p11_m8 minutes_communityservice 

*looking for work
rename p2_1 foreignwork
rename p2_2 localwork
rename p2_3 selfemployed_withoutpay
rename p2_4 notsearching
rename p2a_dia firstsearchdate
replace firstsearchdate = . if firstsearchdate == 99
rename p2a_sem firstsearchweek
replace firstsearchweek = . if firstsearchweek == 9
rename p2a_mes firstsearchmonth
replace firstsearchmonth = . if firstsearchmonth == 99
rename p2a_anio firstsearchyear
replace firstsearchyear = . if firstsearchyear == 9999
rename p2b_dia lastsearchdate
replace lastsearchdate = . if lastsearchdate == 99
rename p2b_sem lastsearchweek
replace lastsearchweek = . if lastsearchweek == 9
rename p2b_mes lastsearchmonth
replace lastsearchmonth =. if lastsearchmonth == 99
rename p2b_anio lastsearchyear
replace lastsearchyear = . if lastsearchyear == 9999
rename p2g2 reasonnotsearching

*work
rename p2f needtowork
replace needtowork = . if needtowork == 9
rename p3i hascontract
replace hascontract = . if hascontract == 9
rename p3b selfemployed
rename p3h recievepay
rename p3k1 recievebonus
rename p3k2 paidvacation
rename p5e reason_noworklw
replace reason_noworklw = . if reason_noworklw == 99
rename p6d jobhealthbenefits
replace jobhealthbenefits=. if jobhealthbenefits == 9
keep v_sel fac age cd_a ent con h_mud r_def n_hog n_ren upm workedlw hasjob jobsector hoursworkedlw daysworkedlw averagehours totalhours daysandhours totaldays urbanrural lastyearworked lastmonthworked foreignwork localwork selfemployed notsearching firstsearchdate firstsearchweek firstsearchmonth firstsearchyear lastsearchdate lastsearchmonth lastsearchweek lastsearchyear reasonnotsearching needtowork hascontract selfemployed_withoutpay recievepay recievebonus paidvacation reason_noworklw jobhealthbenefits studying hours_studying minutes_studying care_for_family hours_care minutes_care home_purchases hours_purchases minutes_purchases walk_family_toschool hours_walktoschool minutes_walktoschool home_construction hours_construction minutes_construction home_repair hours_repair minutes_repair homechores hours_chores minutes_chores community_service hours_communityservice minutes_communityservice 

merge 1:1 cd_a ent con v_sel n_hog h_mud n_ren using "2021_Q1_DEMOGRAPHICS.dta"
save "2021_q1.dta", replace 


*2021 QUARTER 3//SEPTEMBER

use "enoen_hogt321.dta"

keep d_dia d_mes d_anio cd_a ent con v_sel tipo mes_cal ca n_hog h_mud 

merge 1:m v_sel n_hog h_mud cd_a ent con tipo mes_cal ca using "enoen_sdemt321.dta"

*New labels 
rename sex gender 
rename eda age
replace age = . if age == 99
rename nac_dia birthday
replace birthday = . if birthday == 99
rename nac_mes birthmonth
replace birthmonth = . if birthmonth == 99
rename nac_anio birthyear
replace birthyear = . if birthyear == 9999
rename cs_nr_ori stateeducation
rename eda19c agegroups
*education
rename cs_p13_1 degreecompleted
replace degreecompleted = . if degreecompleted == 9
rename cs_p13_2 yearscompleted 
label var yearscompleted "Years finished at schooling level"
rename cs_p16 finishedstudies
replace finishedstudies = . if finishedstudies == 9 
rename anios_esc  yearsofschool
rename cs_p12 readandwrite
rename cs_p17 attendedschool
*Work
rename hrsocup hoursperweek
rename ingocup  monthlyincome
rename ing_x_hrs incomeperhour
rename salario monthlysalary
rename ing7c incomelevels
rename p14apoyos supportprograms
rename clase3 employednopay
*family
rename n_hij children
replace children = . if children == 99
rename e_con marriagestatus
replace marriagestatus = . if marriagestatus == 9 
keep r_def cd_a ent con v_sel h_mud n_hog tipo mes_cal ca upm n_ren fac_tri fac_men mun loc t_loc_tri t_loc_men gender age birthday birthmonth degreecompleted stateeducation yearscompleted finishedstudies yearsofschool readandwrite attendedschool hoursperweek monthlyincome incomeperhour monthlysalary incomelevels supportprograms employednopay agegroups children marriagestatus d_dia d_mes d_anio 

save 2021_Q3_DEMOGRAPHICS.dta, replace 

use "enoen_coe1t321.dta"

merge 1:1 v_sel n_hog h_mud cd_a ent con tipo mes_cal ca  n_ren using "enoen_coe2t321.dta"

rename eda age
rename p1 workedlw
rename p1b hasjob
rename p4d1 jobsector
replace jobsector = . if jobsector == 9
rename p5b_thrs hoursworkedlw
replace hoursworkedlw = . if hoursworkedlw == 999
rename p5b_tdia daysworkedlw
replace daysworkedlw =. if daysworkedlw == 9
rename p5c averagehours
replace averagehours = . if averagehours== 9
rename p5d_thrs totalhours
replace totalhours = . if totalhours == 999
rename p5d_tdia totaldays
replace totaldays=. if totaldays == 9
rename ur urbanrural
rename p2k_anio lastyearworked
replace lastyearworked = . if lastyearworked == 9999
rename p2k_mes lastmonthworked
replace lastmonthworked = . if lastmonthworked == 99
rename p5d1 daysandhours 

*Other activities 
rename p9_1 studying 
rename p9_h1 hours_studying
rename p9_m1 minutes_studying 
rename p9_2 care_for_family 
rename p9_h2 hours_care 
rename p9_m2 minutes_care 
rename p9_3 home_purchases 
rename p9_h3 hours_purchases 
rename p9_m3 minutes_purchases 
rename p9_4 walk_family_toschool
rename p9_h4 hours_walktoschool
rename p9_m4 minutes_walktoschool
rename p9_5 home_construction
rename p9_h5 hours_construction
rename p9_m5 minutes_construction 
rename p9_6 home_repair 
rename p9_h6 hours_repair 
rename p9_m6 minutes_repair 
rename p9_7 homechores 
rename p9_h7 hours_chores
rename p9_m7 minutes_chores 
rename p9_8 community_service 
rename p9_h8 hours_communityservice
rename p9_m8 minutes_communityservice 

*looking for work
rename p2_1 foreignwork
rename p2_2 localwork
rename p2_3 selfemployed_withoutpay
rename p2_4 notsearching
rename p2a_dia firstsearchdate
replace firstsearchdate = . if firstsearchdate == 99
rename p2a_sem firstsearchweek
replace firstsearchweek = . if firstsearchweek == 9
rename p2a_mes firstsearchmonth
replace firstsearchmonth = . if firstsearchmonth == 99
rename p2a_anio	firstsearchyear
replace firstsearchyear = . if firstsearchyear == 9999
rename p2b_dia lastsearchdate
replace lastsearchdate = . if lastsearchdate == 99
rename p2b_sem lastsearchweek
replace lastsearchweek = . if lastsearchweek == 9
rename p2b_mes lastsearchmonth
replace lastsearchmonth =. if lastsearchmonth == 99
rename p2b_anio lastsearchyear
replace lastsearchyear = . if lastsearchyear == 9999
rename p2g2 reasonnotsearching

*work
rename p2f needtowork
replace needtowork = . if needtowork == 9
rename p3i hascontract
replace hascontract = . if hascontract == 9
rename p3b selfemployed
rename p3h recievepay
rename p3k1 recievebonus
rename p3k2 paidvacation
rename p5e reason_noworklw
replace reason_noworklw = . if reason_noworklw == 99
rename p6d jobhealthbenefits
replace jobhealthbenefits=. if jobhealthbenefits == 9
keep v_sel fac_tri fac_men age cd_a ent con h_mud r_def n_hog n_ren tipo mes_cal ca upm workedlw hasjob jobsector hoursworkedlw daysworkedlw averagehours totalhours daysandhours totaldays urbanrural lastyearworked lastmonthworked foreignwork localwork selfemployed notsearching firstsearchdate firstsearchweek firstsearchmonth firstsearchyear lastsearchdate lastsearchmonth lastsearchweek lastsearchyear reasonnotsearching needtowork hascontract selfemployed_withoutpay recievepay recievebonus paidvacation reason_noworklw jobhealthbenefits studying hours_studying minutes_studying care_for_family hours_care minutes_care home_purchases hours_purchases minutes_purchases walk_family_toschool hours_walktoschool minutes_walktoschool home_construction hours_construction minutes_construction home_repair hours_repair minutes_repair homechores hours_chores minutes_chores community_service hours_communityservice minutes_communityservice 

merge 1:1 v_sel n_hog h_mud cd_a ent con tipo mes_cal ca  n_ren using "2021_Q3_DEMOGRAPHICS.dta"

save 2021_Q3.dta, replace

*2022 QUARTER 1
use "hogt122.dta"
keep D_MES D_DIA D_ANIO CD_A ENT CON V_SEL N_HOG H_MUD

merge 1:m CD_A ENT CON V_SEL N_HOG H_MUD using "sdemt122.dta"

rename D_MES d_mes
rename D_DIA d_dia 
rename D_ANIO d_anio
rename UPM upm
rename CON con
rename R_DEF r_def
rename CD_A cd_a
rename ENT ent
rename N_HOG n_hog
rename H_MUD h_mud
rename N_REN n_ren
rename V_SEL v_sel
rename MUN mun
rename FAC fac

rename SEX gender 
rename LOC loc
rename T_LOC t_loc
rename EDA age 
rename NAC_DIA birthday
destring birthday, replace 
replace birthday = . if birthday == 99
rename NAC_MES birthmonth
destring birthmonth, replace 
replace birthmonth = . if birthmonth == 99
rename NAC_ANIO birthyear
destring birthyear, replace 
replace birthyear = . if birthyear == 9999
rename CS_NR_ORI stateeducation
rename EDA19C agegroups
*education
rename CS_P13_1 degreecompleted
replace degreecompleted = . if degreecompleted == 9
rename CS_P13_2 yearscompleted 
label var yearscompleted "Years finished at schooling level"
rename CS_P16 finishedstudies
replace finishedstudies = . if finishedstudies == 9 
rename ANIOS_ESC yearsofschool
rename CS_P12 readandwrite
rename CS_P17 attendedschool
*Work
rename HRSOCUP hoursperweek
rename INGOCUP monthlyincome
rename ING_X_HRS incomeperhour
rename SALARIO monthlysalary
rename ING7C incomelevels
rename P14APOYOS supportprograms
rename CLASE3 employednopay
*family
rename N_HIJ children
replace children = . if children == 99
rename E_CON marriagestatus
replace marriagestatus = . if marriagestatus == 9 
keep r_def cd_a ent con v_sel h_mud n_hog upm n_ren fac mun loc t_loc gender age birthday birthmonth degreecompleted stateeducation yearscompleted finishedstudies yearsofschool readandwrite attendedschool hoursperweek monthlyincome incomeperhour monthlysalary incomelevels supportprograms employednopay agegroups children marriagestatus d_dia d_mes d_anio 

save 2022_quarter1_DEMOGRAPHICS.dta, replace
clear

use "coe1t122.dta"

rename R_DEF r_def 
rename CD_A cd_a
rename D_SEM d_sem
rename V_SEL v_sel
rename N_HOG n_hog
rename H_MUD h_mud
rename N_ENT n_ent
rename N_REN n_ren
rename ENT ent 
rename CON con 
rename UPM upm
rename PER per
rename N_PRO_VIV n_pro_viv
rename FAC fac
merge 1:1 cd_a ent con n_hog h_mud n_ren v_sel using "coe2t119.dta"

*identifiers
rename EDA age
rename P1 workedlw
rename P1B hasjob
rename P4D1 jobsector
replace jobsector = . if jobsector == 9
rename P5C_THRS hoursworkedlw
replace hoursworkedlw = . if hoursworkedlw == 999
rename P5C_TDIA daysworkedlw
replace daysworkedlw =. if daysworkedlw == 9
rename P5D averagehours
replace averagehours = . if averagehours== 9
rename P5E_THRS totalhours
replace totalhours = . if totalhours == 999
rename P5E_TDIA totaldays
replace totaldays=. if totaldays == 9
rename UR urbanrural
rename p9f_anio lastyearworked
replace lastyearworked = . if lastyearworked == 9999
rename p9f_mes lastmonthworked
replace lastmonthworked = . if lastmonthworked == 99
rename P5E1 daysandhours 

*Other activities 
rename p11_1 studying 
rename p11_h1 hours_studying
rename p11_m1 minutes_studying 
rename p11_2 care_for_family 
rename p11_h2 hours_care 
rename p11_m2 minutes_care 
rename p11_3 home_purchases 
rename p11_h3 hours_purchases 
rename p11_m3 minutes_purchases 
rename p11_4 walk_family_toschool
rename p11_h4 hours_walktoschool
rename p11_m4 minutes_walktoschool
rename p11_5 home_construction
rename p11_h5 hours_construction
rename p11_m5 minutes_construction 
rename p11_6 home_repair 
rename p11_h6 hours_repair 
rename p11_m6 minutes_repair 
rename p11_7 homechores 
rename p11_h7 hours_chores
rename p11_m7 minutes_chores 
rename p11_8 community_service 
rename p11_h8 hours_communityservice
rename p11_m8 minutes_communityservice 

*looking for work
rename P2_1 foreignwork
rename P2_2 localwork
rename P2_3 selfemployed_withoutpay
rename P2_4 notsearching

rename P2A_DIA firstsearchdate
replace firstsearchdate = . if firstsearchdate == 99
rename P2A_SEM firstsearchweek
replace firstsearchweek = . if firstsearchweek == 9
rename P2A_MES firstsearchmonth
replace firstsearchmonth = . if firstsearchmonth == 99
rename P2A_ANIO firstsearchyear
replace firstsearchyear = . if firstsearchyear == 9999

rename P2B_DIA lastsearchdate
replace lastsearchdate = . if lastsearchdate == 99
rename P2B_SEM lastsearchweek
replace lastsearchweek = . if lastsearchweek == 9
rename P2B_MES lastsearchmonth
replace lastsearchmonth =. if lastsearchmonth == 99
rename P2B_ANIO lastsearchyear
replace lastsearchyear = . if lastsearchyear == 9999
rename P2G2 reasonnotsearching

*work
rename P2F needtowork
replace needtowork = . if needtowork == 9
rename P3J hascontract
replace hascontract = . if hascontract == 9
rename P3B selfemployed
rename P3H recievepay
rename P3L1 recievebonus
rename P3L2 paidvacation
rename P5F reason_noworklw
replace reason_noworklw = . if reason_noworklw == 99
rename p6d jobhealthbenefits
replace jobhealthbenefits=. if jobhealthbenefits == 9
rename p10_1 jobassistance 
replace jobassistance=0 if jobassistance==.
rename p10_2 microcredit
replace microcredit=0 if microcredit==.
rename p10_3 othergovprogram
replace othergovprogram=0 if othergovprogram==.
rename p10_4 nogovassistance
replace nogovassistance=0 if nogovassistance==.

keep v_sel fac age cd_a ent con h_mud r_def n_hog n_ren upm workedlw hasjob jobsector hoursworkedlw daysworkedlw averagehours totalhours daysandhours totaldays urbanrural lastyearworked lastmonthworked foreignwork localwork selfemployed notsearching firstsearchdate firstsearchweek firstsearchmonth firstsearchyear lastsearchdate lastsearchmonth lastsearchweek lastsearchyear reasonnotsearching needtowork hascontract selfemployed_withoutpay recievepay recievebonus paidvacation reason_noworklw jobhealthbenefits studying hours_studying minutes_studying care_for_family hours_care minutes_care home_purchases hours_purchases minutes_purchases walk_family_toschool hours_walktoschool minutes_walktoschool home_construction hours_construction minutes_construction home_repair hours_repair minutes_repair homechores hours_chores minutes_chores community_service hours_communityservice minutes_communityservice jobassistance microcredit othergovprogram nogovassistance

merge 1:1 cd_a ent con v_sel n_hog h_mud n_ren using "2022_quarter1_DEMOGRAPHICS.dta"

save 2022_quarter1.dta, replace 


*2022 QUARTER 3//SEPTEMBER

use "enoen_hogt322.dta"

keep d_dia d_mes d_anio cd_a ent con v_sel tipo mes_cal ca n_hog h_mud 

merge 1:m v_sel n_hog h_mud cd_a ent con tipo mes_cal ca using "enoen_sdemt322.dta"

*New labels 
rename sex gender 
rename eda age
replace age = . if age == 99
rename nac_dia birthday
replace birthday = . if birthday == 99
rename nac_mes birthmonth
replace birthmonth = . if birthmonth == 99
rename nac_anio birthyear
replace birthyear = . if birthyear == 9999
rename cs_nr_ori stateeducation
rename eda19c agegroups
*education
rename cs_p13_1 degreecompleted
replace degreecompleted = . if degreecompleted == 9
rename cs_p13_2 yearscompleted 
label var yearscompleted "Years finished at schooling level"
rename cs_p16 finishedstudies
replace finishedstudies = . if finishedstudies == 9 
rename anios_esc  yearsofschool
rename cs_p12 readandwrite
rename cs_p17 attendedschool
*Work
rename hrsocup hoursperweek
rename ingocup  monthlyincome
rename ing_x_hrs incomeperhour
rename salario monthlysalary
rename ing7c incomelevels
rename p14apoyos supportprograms
rename clase3 employednopay
*family
rename n_hij children
replace children = . if children == 99
rename e_con marriagestatus
replace marriagestatus = . if marriagestatus == 9 
keep r_def cd_a ent con v_sel h_mud n_hog tipo mes_cal ca upm n_ren fac_tri fac_men mun loc t_loc_tri t_loc_men gender age birthday birthmonth degreecompleted stateeducation yearscompleted finishedstudies yearsofschool readandwrite attendedschool hoursperweek monthlyincome incomeperhour monthlysalary incomelevels supportprograms employednopay agegroups children marriagestatus d_dia d_mes d_anio 

save 2022_Q3_DEMOGRAPHICS.dta, replace 

use "enoen_coe1t322.dta"

merge 1:1 v_sel n_hog h_mud cd_a ent con tipo mes_cal ca  n_ren using "enoen_coe2t322.dta"

rename eda age
rename p1 workedlw
rename p1b hasjob
rename p4d1 jobsector
replace jobsector = . if jobsector == 9
rename p5b_thrs hoursworkedlw
replace hoursworkedlw = . if hoursworkedlw == 999
rename p5b_tdia daysworkedlw
replace daysworkedlw =. if daysworkedlw == 9
rename p5c averagehours
replace averagehours = . if averagehours== 9
rename p5d_thrs totalhours
replace totalhours = . if totalhours == 999
rename p5d_tdia totaldays
replace totaldays=. if totaldays == 9
rename ur urbanrural
rename p2k_anio lastyearworked
replace lastyearworked = . if lastyearworked == 9999
rename p2k_mes lastmonthworked
replace lastmonthworked = . if lastmonthworked == 99
rename p5d1 daysandhours 

*Other activities 
rename p9_1 studying 
rename p9_h1 hours_studying
rename p9_m1 minutes_studying 
rename p9_2 care_for_family 
rename p9_h2 hours_care 
rename p9_m2 minutes_care 
rename p9_3 home_purchases 
rename p9_h3 hours_purchases 
rename p9_m3 minutes_purchases 
rename p9_4 walk_family_toschool
rename p9_h4 hours_walktoschool
rename p9_m4 minutes_walktoschool
rename p9_5 home_construction
rename p9_h5 hours_construction
rename p9_m5 minutes_construction 
rename p9_6 home_repair 
rename p9_h6 hours_repair 
rename p9_m6 minutes_repair 
rename p9_7 homechores 
rename p9_h7 hours_chores
rename p9_m7 minutes_chores 
rename p9_8 community_service 
rename p9_h8 hours_communityservice
rename p9_m8 minutes_communityservice 

*looking for work
rename p2_1 foreignwork
rename p2_2 localwork
rename p2_3 selfemployed_withoutpay
rename p2_4 notsearching
rename p2a_dia firstsearchdate
replace firstsearchdate = . if firstsearchdate == 99
rename p2a_sem firstsearchweek
replace firstsearchweek = . if firstsearchweek == 9
rename p2a_mes firstsearchmonth
replace firstsearchmonth = . if firstsearchmonth == 99
rename p2a_anio	firstsearchyear
replace firstsearchyear = . if firstsearchyear == 9999
rename p2b_dia lastsearchdate
replace lastsearchdate = . if lastsearchdate == 99
rename p2b_sem lastsearchweek
replace lastsearchweek = . if lastsearchweek == 9
rename p2b_mes lastsearchmonth
replace lastsearchmonth =. if lastsearchmonth == 99
rename p2b_anio lastsearchyear
replace lastsearchyear = . if lastsearchyear == 9999
rename p2g2 reasonnotsearching

*work
rename p2f needtowork
replace needtowork = . if needtowork == 9
rename p3i hascontract
replace hascontract = . if hascontract == 9
rename p3b selfemployed
rename p3h recievepay
rename p3k1 recievebonus
rename p3k2 paidvacation
rename p5e reason_noworklw
replace reason_noworklw = . if reason_noworklw == 99
rename p6d jobhealthbenefits
replace jobhealthbenefits=. if jobhealthbenefits == 9
keep v_sel fac_tri fac_men age cd_a ent con h_mud r_def n_hog n_ren tipo mes_cal ca upm workedlw hasjob jobsector hoursworkedlw daysworkedlw averagehours totalhours daysandhours totaldays urbanrural lastyearworked lastmonthworked foreignwork localwork selfemployed notsearching firstsearchdate firstsearchweek firstsearchmonth firstsearchyear lastsearchdate lastsearchmonth lastsearchweek lastsearchyear reasonnotsearching needtowork hascontract selfemployed_withoutpay recievepay recievebonus paidvacation reason_noworklw jobhealthbenefits studying hours_studying minutes_studying care_for_family hours_care minutes_care home_purchases hours_purchases minutes_purchases walk_family_toschool hours_walktoschool minutes_walktoschool home_construction hours_construction minutes_construction home_repair hours_repair minutes_repair homechores hours_chores minutes_chores community_service hours_communityservice minutes_communityservice 

merge 1:1 v_sel n_hog h_mud cd_a ent con tipo mes_cal ca  n_ren using "2022_Q3_DEMOGRAPHICS.dta"

save 2022_Q3.dta, replace
