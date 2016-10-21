---
ID: 576
post_title: >
  Awk Snippet for Extracting XML Messages
  with a Given ID from a Log File
author: Luc
post_date: 2015-03-27 18:55:55
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/snippet-for-extracting-xml-messages-log-file/
published: true
---
I recently had occasion to extract XML messages with a specific id from log files, resulting in the following gnarly awk snippet. The sed statement at the end is for stripping out some unwanted debug statements. There must be a better way to do this, let me know in the comments (except don't, because they are disabled, because apparently only spammers read this blog).


 
<pre class="lang:sh decode:true "  >#$1 id tag (e.g. if the identifier is specified with &lt;id&gt;1234&lt;/id&gt;, use id)
#$2 id (e.g. if the identifier is enclosed with &lt;id&gt;1234&lt;/id&gt;, use id)
#$3 message separator (e.g. &lt;/message&gt;)
#$4 file prefix (e.g. if there are multiple messages in the file with the same id, use this prefix when writing out the resulting files)
#$5 log file (the name of the file to read)
extract_message(){
	awk -v var="&lt;${1}&gt;${2}&lt;\\\/${1}&gt;"  \
		-v ORS="&lt;/${3}&gt;\n" \
		-v RS="&lt;\\\/${3}&gt;"  \
		'$0 ~ var {print}' $5 | sed 's/^[0-9][0-9].*DEBUG.*&lt;/&lt;/' \
		| awk -v pre="${4}" '{print $0 &gt; pre NR}' RS='\\n\\n' -	
}
</pre>