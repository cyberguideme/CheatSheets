# Analyzing Malicious Documents Cheat Sheet

This cheat sheet outlines tips and tools for reverse-engineering malicious documents, such as Microsoft Office (DOC, XLS, PPT) and Adobe Acrobat (PDF) files.

## General Approach

1.  Locate potentially malicious embedded code, such as shellcode, VBA macros, or JavaScript.
2.  Extract suspicious code segments from the file.
3.  If relevant, disassemble and/or debug shellcode.
4.  If relevant, deobfuscate and examine JavaScript, ActionScript, or VB macro code.
5.  Understand next steps in the infection chain.

## Microsoft Office Binary File Format Notes

Structured Storage (OLE SS) defines a file system inside the binary Microsoft Office file.

Data can be “storage” (folder) and “stream” (file).

Excel stores data inside the “workbook” stream.

PowerPoint stores data inside the “PowerPoint Document” stream.

Word stores data inside various streams.

## Tools for Analyzing Microsoft Office Files

[OfficeMalScanner](http://www.reconstructer.org/code/OfficeMalScanner.zip)  locates shellcode and VBA macros from MS Office (DOC, XLS, and PPT) files.

MalHost-Setup extracts shellcode from a given offset in an MS Office file and embeds it an EXE file for further analysis. (Part of  [OfficeMalScanner](http://www.reconstructer.org/code/OfficeMalScanner.zip))

[Offvis](http://go.microsoft.com/fwlink/?LinkId=158791)  shows raw contents and structure of an MS Office file, and identifies some common exploits.

[Hachoir-urwid](https://bitbucket.org/haypo/hachoir/wiki/hachoir-urwid)  can navigate through the structure of binary Office files and view stream contents.

[Office Binary Translator](http://b2xtranslator.sourceforge.net/)  converts DOC, PPT, and XLS files into Open XML files (includes  [BiffView](http://b2xtranslator.sourceforge.net/snapshots/BiffView.zip)  tool).

pyOLEScanner.py can examine and decode some aspects of malicious binary Office files.

[FileHex](http://www.heaventools.com/)  (not free) and  [FileInsight](http://vil.nai.com/vil/averttools.aspx)  hex editors can parse and edit OLE structures.

## Useful MS Office Analysis Commands

OfficeMalScanner  _file.doc_  scan brute

Locate shellcode, OLE data, PE files in  _file.doc_

OfficeMalScanner  _file.doc_  info

Locate VB macro code in  _file.doc_  (no XML files)

OfficeMalScanner  _file.docx_  inflate

Decompress  _file.docx_  to locate VB code (XML files)

MalHost-Setup  _file.doc_  _out.exe_  0x4500

Extract shellcode from  _file.doc_’s offset 0x4500 and create it as  _out.exe_

## Adobe PDF File Format Notes

A PDF File is comprised of header, objects, cross-reference table (to locate objects), and trailer.

“/OpenAction” and “/AA” (Additional Action) specifies the script or action to run automatically.

“/Names”, “/AcroForm”, “/Action” can also specify and launch scripts or actions.

“/JavaScript” specifies JavaScript to run.

“/GoTo*” changes the view to a specified destination within the PDF or in another PDF file.

“/Launch” launches a program or opens a document.

“/URI” accesses a resource by its URL.

“/SubmitForm” and “/GoToR” can send data to URL.

“/RichMedia” can be used to embed Flash in PDF.

“/ObjStm” can hide objects inside an Object Stream.

Be mindful of obfuscation with hex codes, such as “/JavaScript” vs. “/J#61vaScript”. ([See examples](http://blog.didierstevens.com/2008/04/29/pdf-let-me-count-the-ways/))

## Tools for Analyzing Adobe PDF Files

[PDFiD](http://blog.didierstevens.com/programs/pdf-tools/)  identifies PDFs that contain strings associated with scripts and actions.

[PDF-parser](http://blog.didierstevens.com/programs/pdf-tools/)  and  [Origami’s](http://security-labs.org/origami/)  pdfwalker examines the structure of PDF files.

[Origami’s](http://security-labs.org/origami/)  pdfextract and  [Jsunpack-n’s](http://jsunpack.blogspot.com/2009/06/jsunpack-n-updates-for-pdf-decoding.html)  pdf.py extract JavaScript from PDF files.

[PDF Stream Dumper](http://blog.zeltser.com/post/3235995383/pdf-stream-dumper-malicious-file-analysis)  combines many PDF analysis tools under a single graphical user interface.

[Peepdf](http://blog.zeltser.com/post/6780160077/peepdf-malicious-pdf-analysis)  and  [Origami’s](http://esec-lab.sogeti.com/pages/Origami)  pdfsh offer an interactive command-line shell for examining PDF files.

[PDF X-RAY Lite](https://github.com/9b/pdfxray_lite)  creates an HTML report containing decoded PDF file structure and contents.

[SWF mastah](http://blog.zeltser.com/post/12615013257/extracting-swf-from-pdf-using-swf-mastah)  extracts SWF objects from PDF files.

[Pyew](http://code.google.com/p/pyew/wiki/PDFAnalysis)  includes commands for examining and decoding structure and content of PDF files.

## Useful PDF Analysis Commands

pdfid.py  _file.pdf_

Locate script and action-related strings in  _file.pdf_

pdf-parser.py  _file.pdf_

Show  _file.pdf_’s structure to identify suspect elements

pdf-parser.py --object  _id_  _file.pdf_

Display contents of object  _id_  in  _file.pdf_. Add “--filter --raw” to decode the object’s stream.

pdfextract  _file.pdf_

Extract JavaScript embedded in  _file.pdf_  and save it to  _file.dump_.

pdf.py  _file.pdf_

Extract JavaScript embedded in  _file.pdf_  and save it to  _file.pdf.out_.

swf_mastah.py –f  _file.pdf_  
–o  _out_

Extract PDF objects from  _file.pdf_  into the  _out_  directory.

## Additional PDF Analysis Tools

[Malzilla](http://www.malzilla.org/)  and  [SpiderMonkey](http://isc.sans.edu/diary.html?storyid=12157)  can help deobfuscate JavaScript embedded in malicious PDF files.

[Wepawet](http://wepawet.cs.ucsb.edu/),  [Jsunpack](http://jsunpack.jeek.org/dec/go),  [VirusTotal](http://www.virustotal.com/)  and  [sandbox tools](http://zeltser.com/reverse-malware/automated-malware-analysis.html)  can analyze some aspects of malicious PDF files.

[ExeFilter](http://www.decalage.info/exefilter)  can filter scripts from Office and PDF files.

## References

[Adobe Portable Document Format (PDF) Reference](http://www.adobe.com/devnet/pdf/pdf_reference.html)

[Physical and Logical Structure of PDF Files](http://blog.didierstevens.com/2008/04/09/quickpost-about-the-physical-and-logical-structure-of-pdf-files/)

[Methods for Understanding and Analyzing Targeted Attacks with Office Documents](http://recon.cx/2008/a/bruce_dang/recon08_final.zip)  ([video](http://bork.informatik.uni-erlangen.de/pub/ccc/25c3/video_h264_720x576/25c3-2938-en-methods_for_understanding_targeted_attacks_with_office_documents.mp4))

[Analyzing MSOffice Malware with OfficeMalScanner](http://www.reconstructer.org/papers/Analyzing%20MSOffice%20malware%20with%20OfficeMalScanner.zip)  ([follow-up presentation](http://2009.hack.lu/archive/2009/New%20advances%20in%20Ms%20Office%20malware%20analysis.pdf))

[PDF Security Analysis and Malware Threats](http://www.blackhat.com/presentations/bh-europe-08/Filiol/Presentation/bh-eu-08-filiol.pdf)

[Reverse-Engineering Malware cheat sheet](http://zeltser.com/reverse-malware/reverse-malware-cheat-sheet.html)

[REMnux Linux distribution for malware analysis.](http://remnux.org/)
