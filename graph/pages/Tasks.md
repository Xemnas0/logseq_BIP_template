icon:: ✅

- ## In corso
  background-color:: green
	- {{query (task DOING NOW)}}
	  query-table:: true
- ## In sospeso
  background-color:: purple
	- {{query (task WAITING WAIT)}}
	  query-table:: true
- ## Da fare
	- ### Alta priorità
	  background-color:: red
		- {{query (and (task TODO LATER) (priority A))(task TODO LATER)}}
		  query-table:: true
	- ### Media priorità
	  background-color:: yellow
		- {{query (and (task TODO LATER) (priority B))(task TODO LATER)}}
		  query-table:: true
	- Bassa priorità
	  background-color:: gray
	  heading:: true
		- {{query (and (task TODO LATER) (priority C))(task TODO LATER)}}
		  query-table:: true
	- ### Priorità non assegnata
	  background-color:: blue
		- {{query (and (task TODO LATER) (not (priority A B C)))}}
		  query-table:: true