
#OPPGAVE IND01 

fun
  flag(outer-vertical, inner-vertical, inner-horizontal, outer-horizontal, background) : 
  frame(
  overlay-xy(rectangle(20, 160, "solid", outer-vertical), -75, 0, 
    overlay-xy(rectangle(220, 20, "solid", outer-horizontal), 0, -68, 
      overlay-xy(rectangle(45, 160, "solid", inner-vertical), -62, 0, 
        overlay-xy( rectangle(220, 40, "solid", inner-horizontal), 0, -58, 
            rectangle(220, 160, "solid", background))))))

#Her har jeg definert de ulike delene i flagdelene og lagd en formel som du legger inn farger på for å få de ulike flaggene, under ser du de ulike kombinasjonene av farger for å få de ulike nordiske flaggene. 
 

end

#Norwegian flag
flag("blue", "white", "white", "blue", "red")


#Danish flag
flag("white", "red", "red", "white", "red")

#Finnish flag
flag("blue", "blue", "blue", "blue", "white")

#Island
flag("red", "white", "white", "red", "blue")

#Swedish flag
flag("yellow", "blue", "blue", "yellow", "blue")

#Faroe islands
flag("red", "blue", "blue", "red", "white")







include shared-gdrive(
"dcic-2021",
"1wyQZj_L0qqV9Ekgr9au6RX2iqt2Ga8Ep")

#denne blokken laster ned tabbellen

include gdrive-sheets
include data-source
ssid = "1RYN0i4Zx_UETVuYacgaGfnFcv4l9zd9toQTTdkQkj7g"
kwh-table =
load-table: komponent, energi
source: load-spreadsheet(ssid).sheet-by-name("kWh", true)
    sanitize energi using string-sanitizer
end


# a)her har jeg kallt tabellen for kwh-table for å gjøre det enklere. første steg er også å sanitere energi kolonnen for å få dataen i string form, fra ubestemt form. 


kwh-table
#skriver tabellen i command for å få den opp i feltet. 


fun energi-to-number(str :: String) -> Number:
  cases(Option) string-to-number(str):
    | some(a) => a
    | none => 20
  end  
where: 
  energi-to-number("") is 0
  energi-to-number("48") is 48
  energi-to-number("35") is 35
end

# b) Denne funksjonen gjør strenger (altså tall) i anførselstegn om til vanlig tall, ved hjelp av string-to-number funksjonen. Her bruker jeg også cases(Option) for å gjøre slik at det ikke blir gitt i  some(12) eller none. Det er også gitt where eksempler for å sjekke at funksjonen gjør det riktig. 

kwh-table2 = transform-column(kwh-table, "energi", energi-to-number)

kwh-table2

# C) her bruker jeg transoform-column funksjonen for å gjøre om strengene under energi i kwh tabellen ved hjelp av funksjonen jeg lagde over. gir den også en definisjon slik at jeg kan bruke den videre. 

sum(kwh-table2, "energi")

# d) her bruker jeg sum funksjonen for å summere all energikravet til en innbygger ved å summere energi kolonnen. da får jeg svaret 155 fra vinduet. Deretter vil jeg regne ut energi kravet til bilen også summere disse igjen for å få det endelige svaret. 

distance-travelled-per-day = 20
distance-per-unit-of-fuel = 10
energy-per-unit-of-fuel = 10

energy-per-day = ( distance-travelled-per-day / 
                            distance-per-unit-of-fuel ) * 
                                        energy-per-unit-of-fuel
energy-per-day

# d) her har jeg brukt regnestykket gitt fra kompendiumet og lagt til verdier som vil være realistiske. Da gir energy-per-day 20. summerer vi da disse to står vi igjen med ett totalt forbruk på 175 kwh. 




# e) For å visualisere dette, bruker vi bar chart, men først gjør jeg en endring i energi-to-number funksjonen. Da endrer jeg [none => 0] til [none => 20]. Dette er fordi bil forbruket er 20 og bil er den eneste som har verdien none i tabellen, den vil da få riktig verdi vedd å "jukse" litt. 


bar-chart(kwh-table2, "komponent","energi")


# e) Deretter lager jeg en bar chart nå som vi har informasjon inne. den ser slik ut: 