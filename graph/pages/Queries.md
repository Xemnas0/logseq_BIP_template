icon:: 🔍

- ## Consuntivi
	- #+BEGIN_QUERY
	  {:title [:h2 "Consuntivo dei 35 giorni precedenti"]
	      :query [
	          :find (pull ?b [ {:block/page
	       [:block/name :block/journal-day]} :block/properties])
	          :in $ ?start ?today
	          :where
	          [?b :block/properties ?prop]
	          [(get ?prop :type) ?type]
	          [(= ?type "consuntivo")]
	          [?p :block/journal-day ?d]
	          [(>= ?d ?start)]
	          [(<= ?d ?today)]
	          [?b :block/page ?p]
	          (not [?b :page/name "templates"])    ]
	      :inputs [:35d :today]
	     :result-transform (fn [result]
	                                     (map
	                                        (fn [m]
	                                            (update m :block/properties (fn [u]
	                                               (assoc u :journal-day (clojure.string/join "/" (rest (re-matches (re-pattern "(\\d{4})(\\d{2})(\\d{2})") (str (get-in m [:block/page :block/journal-day]))))))))) (sort-by (fn [b] (get-in b [:block/page :block/journal-day])) result))
	      )
	  :view (fn [rows] [:table 
	       [:thead 
	        [:tr 
	         [:th {:width "10%"} "Day"] 
	         [:th "Task"]
	         [:th {:width "5%"} "Hours"]
	         [:th "Description"] ] ] 
	       [:tbody 
	      (for [r rows] [:tr 
	         [:td (get-in r [:block/properties :journal-day])] 
	         [:td (get-in r [:block/properties :task])]
	         [:td (get-in r [:block/properties :hours])]
	         [:td (get-in r [:block/properties :description])] ])
	     ]]
	  )
	  }
	  #+END_QUERY}
-