---


---

<h1 id="bitwise---training-ticket---runbook"><strong>Bitwise - Training Ticket - Runbook</strong></h1>
<h2 id="ambiente-di-sviluppo-bitwise-playground">Ambiente di sviluppo: Bitwise playground</h2>
<h3 id="creazione-della-solution">Creazione della Solution</h3>
<p><strong>La solution è stata creata con il display name: Bitwise - Tirocinio,  editor: Bitwise, version 1.0.0.0</strong><br>
<strong>All’interno sono stati creati i seguenti elementi:</strong></p>
<ul>
<li>Tables: <strong>bit_trainingticket</strong></li>
<li>Choices: <strong>bit_choise</strong></li>
<li>Three Web Resources:
<ul>
<li>Web Resource (JScript): <strong>bit_trainingticket_form.js</strong></li>
<li>Web Resource (JScript): <strong>bit_openDialog.js</strong></li>
<li>Web Resource (HTML): <strong>bit_TicketSummary.html</strong></li>
</ul>
</li>
<li>Apps: <strong>CRMHub</strong></li>
<li>Cloud Flows: <strong>bit - Ticket Due Date Reminder</strong></li>
</ul>
<h3 id="table">Table</h3>
<p><strong>Dati iniziali:</strong></p>
<ul>
<li>Display name: <strong>Training Ticket</strong></li>
<li>Schema name: <strong>bit_trainingticket</strong></li>
<li>Primary Name: <strong>bit_name</strong></li>
</ul>
<p><strong>La Table creata ha le seguenti colonne:</strong></p>
<ul>
<li><strong>bit_title:</strong> di tipo Testo (Required)</li>
<li><strong>bit_description:</strong> di tipo Testo multilinea</li>
<li><strong>bit_prority:</strong> di tipo Choice -&gt; (Low/Medium/High)</li>
<li><strong>bit_duedate:</strong> di tipo Data</li>
<li><strong>bit_isblocked:</strong> di tipo Choice -&gt; (Yes/No, default No)</li>
</ul>
<p><strong>Form (Main)</strong><br>
Divisa in 3 sezioni, <strong>la prima contiene</strong>:</p>
<ul>
<li>Name</li>
<li>Owner</li>
<li>title</li>
<li>priority</li>
</ul>
<p><strong>La seconda: (section_Dettagli)</strong></p>
<ul>
<li>description</li>
<li>lastremindersent</li>
</ul>
<p><strong>La terza: (section_Scadenza)</strong></p>
<ul>
<li>isblocked</li>
<li>duedate</li>
</ul>
<p><strong>All’interno di Training Ticket sono state create 4 Bussines Rules</strong></p>
<ul>
<li>Rimuovere obbligatorietà bit_duedate su bit_prirority != High:  la quale toglie il <strong>Required</strong> a <strong>duedate</strong> se <code>bit_pryiorty != "High"</code></li>
<li>obbligatorietà bit_duedate su bit_prirority = High: la quale obbliga <strong>duedate</strong> a <strong>Required</strong> se <code>bit_priority == "High"</code> e mostra un messaggio <strong>"Inserire una scadenza per priorità alta"</strong></li>
<li>Visibilità condizionate su bit_duedate se bit_islocked = Yes (Hide bit_duedate): la quale nasconde il campo <strong>duedate</strong> se <strong>bit_isblocked</strong> = Yes</li>
<li>Visibilità condizionate su bit_duedate se bit_islocked = Yes (Show bit_duedate): la quale mostra il campo <strong>duedate</strong> se <strong>bit_isblocked</strong> = No</li>
</ul>
<h3 id="web-resoursces">Web Resoursces</h3>
<p><strong>bit_trainingticket_form.js</strong><br>
il file Js registra determinati eventi nella Form, nello specifico:</p>
<ul>
<li>bit_priority onChange</li>
<li>bit_duedate onChange</li>
<li>onLoad del Form per le notifiche</li>
</ul>
<p>La Web Resources dopo aver preso il FormContext controlla il campo se <code>bit_pryiorty == 757730002 &amp;&amp; bit_duedate == null</code>,  (757730002 è  il valore numerico riferito alla <strong>bit_choise</strong> = High) se questa condizione  è soddisfatta crea una <strong>form notification</strong> con il messaggio <strong>“Duedate value required”</strong>  ed Id <strong>“bit_due_required”</strong>.<br>
Se invece <code>bit_priority != 757730002</code> rimuove ogni <strong>Form notification</strong> presente.<br>
Se <code>bit_duedate &lt; new Date()</code> crea una <strong>form notification</strong> con il messaggio <strong>“Duedate need to be after today”</strong> ed Id <strong>"bit_due_past"</strong><br>
Se nessuna di queste condizioni è soddisfatta, allora rimuove ogni tipo di <strong>form notification</strong>.</p>
<p><strong>bit_TicketSummary.html</strong><br>
La Web Resource mostra a schermo determinati dati presenti in uno specifico record letti da querystring.<br>
Nello specifico mostra:</p>
<ul>
<li><strong>RecordId</strong></li>
<li><strong>title</strong></li>
</ul>
<p>Tali dati vengono passati tramite l’utilizzo di un <strong>Button: “Apri riepilogo”</strong>, inserito nella command bar di <strong>Training Ticket</strong>, il quale dopo aver selezionato un record, la Web Resource <strong>bit_openDialog.js</strong>, estrae i dati dalla <strong>Row</strong> selezionata e apre un dialog con  <strong>Xrm.Navigation.navigateTo</strong>, inviando i dati via querystring., i quali poi verrano letti e mostrati grazie a  <strong>bit_TicketSummary.html</strong>.</p>

