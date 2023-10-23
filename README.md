# schoolwork



# gir definisjoner til byggeblokkene, slik at det er lettere å sette sammen med alle overlay funksjonene, og koden blir mye kortere.

left-squares = square(124, "solid", "red")
right-rectangles = rectangle(246, 122, "solid", "red")
white-cross-left = square(146, "solid", "white")
white-cross-right = rectangle(262, 146, "solid", "white")
blue-cross = rectangle(440, 320, "solid", "dark blue")

# left squares er de venstre røde firkantene av flagget, right rectangles er de venstre rektanglene og whitecross left and right er det hvite korsset, blue cross er da egentlig bare ett stort blått rektangel. 






put-image(
  overlay-align("left", "top", left-squares, left-squares),

  222,480,
  
  put-image( 
    overlay-align("left", "bottom", left-squares, left-squares),
    
    222,282,
    
    
    put-image(
      overlay-align("right", "top", right-rectangles, right-rectangles),
      
      477,480,
      
      put-image(
        overlay-align("right", "bottom", right-rectangles, right-rectangles),
        
        477,281,

        put-image(
          overlay-align("right", "bottom", white-cross-right, white-cross-right),
         
          470,293,
          
          put-image(
            overlay-align("right", "top", white-cross-right, white-cross-right),
            
            470,467,
          
            put-image(
              overlay-align("left", "bottom", white-cross-left, white-cross-left),
              
              233,293,
              
              put-image(
                overlay-align("left", "top", white-cross-left, white-cross-left),
                
                233,467,

              
           put-image(
            overlay-align("right", "bottom", blue-cross, blue-cross),
            
            380,380,
                  
                  empty-scene(750, 750))))))))))


# bruker empty scene funksjonen for å ha ett ark der jeg kan plassere byggeblokkene som er definert over. Deretter bruker jeg put-image og overlay-align sammen med koordinater for å plassere blokkene på riktig plass. her har jeg puttet de i slik rekkefølge sånn at den blå rektangelen kommer bakerst.
                  
