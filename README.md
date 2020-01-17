##FreemarkerTemplate docs
================================================
	
	1-binding variable: ${variable}
	Example: <a href="${latestProduct.url}">${latestProduct.name}</a>!


	note:- "${latestProduct.url}" if url property is public
	"${latestProduct.getUrl()}"  if url is private property

2-FTL tags: (also known as freemarker directive)
-----------------------------------------------

1) assignment directive
-----------------------
	
	defined variable
	<#assign x = 1>  <#-- create variable x -->
	<#assign x = "plain">
	1. ${x}  <#-- we see the plain var. here -->


2) condition directive
---------------------
	1) <#if> tag;

	 Welcome ${user}<#if user == "Big Joe">, our beloved leader</#if>!
	 
	 <#if animals.python.price == 0>
	  Pythons are free today!
	</#if>
	<#if animals.python.price < animals.elephant.price>
	  Pythons are cheaper than elephants today.
	<#else>
	  Pythons are not cheaper than elephants today.
	</#if>
	
	<#if animals.python.price < animals.elephant.price>
	  Pythons are cheaper than elephants today.
	<#elseif animals.elephant.price < animals.python.price>
	  Elephants are cheaper than pythons today.
	<#else>
	  Elephants and pythons cost the same today.
	</#if>

	If you have a variable with boolean value (a true/false thing) 
	then you can use it directly as the condition of if:
	<#if animals.python.protected>
	  Pythons are protected animals!
	</#if>


3) loop directive
-----------------

	The list directive(for looping)
	=============================
	<#list animals as animal>
	    <tr><td>${animal.name}<td>${animal.price} Euros
	  </#list>
	
	<#list misc.fruits as fruit>
	  <li>${fruit}
	</#list>
	
	Note-FTL tag also can written in side html tag as atrribute:
	<#list animals as animal>
	      <div<#if animal.protected> class="protected"</#if>>
	        ${animal.name} for ${animal.price} Euros
	      </div>
	</#list>
	
	
4) include directive
-------------------

	<#include "/copyright_footer.html">
	<#include "/common/copyright.ftl">

	
dealing with missing variables
--------------------------------

	h1>Welcome ${user!"visitor"}!</h1>
	if user is missing it will print visitor
	
	3-FTL comments: Directive tags:
	<#-- we see the plain var. here -->
	
	
	example:==
	1-:for list fetching
	===================
	<#if types??>
	  <#list types as type>
	   ${type.name}
	  </#list>
	 </#if>
	 



dealing to accessing i18n messages
-----------------------------------
	spring-mvc-*.jar provide a variable called.springMacroRequestContext
	that is reference of object "org.springframework.web.servlet.support.RequestContext"
	in class "AbstractTemplateView" you can see this hard-core variable passing to template.
	
	using methods of this object can be display the 18n message.
	${springMacroRequestContext.getMessage(code, text)}

directive style to fetch i18n messages
---------------------------------------
	There is user defined macro build by spring- spring.ftl .
	if this is not working you can  create your own user-defined directive

user_define directive
---------------------------
	<#macro directive_name var1 var2...>
	
	body of directives
	
	</#macro>


calling way to userdefined directive
-------------------------------------
	<@directive_name var1="valu1".../>




my example:
-----------
	####defining macro
	---------------------------
	<#macro greet person>
	  Hello ${person}!
	</#macro>

	####calling macro
	--------------
	<@greet person="Fred"/> 











