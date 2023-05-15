icon:: 🧩

- {{renderer :tocgen2}}
- # Pages
	- ## Project
	  template:: project_template
	  template-including-parent:: false
		- type:: project
		  client:: _
		  description:: _
		  status:: ongoing
		  tags::
		- ## Scope
			- _
		- ## Tasks
			- _
		- ## Meetings
			- {{query (and <% current page %> [[meeting]])}}
			  query-properties:: [:block]
	- ## Client
	  template:: client_template
	  template-including-parent:: false
		- type:: company
		  tags::
		- ## Description
			- _
		- ## People
			- {{query (and (page-property :type "person") (page-property :company <% current page %>))}}
			  query-properties:: [:page]
		- ## Project
			- {{query (and (page-property :type "project") (page-property :client <% current page %>))}}
			  query-properties:: [:page]
	- ## Person
	  template:: person_template
	  template-including-parent:: false
		- type:: person
		  company:: _
- # Blocks
	- ## Consuntivo
		- type:: consuntivo
		  task:: _
		  description:: _
		  hours:: 8
		  template:: consuntivo_template