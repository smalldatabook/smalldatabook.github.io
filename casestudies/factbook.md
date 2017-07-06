# World Factbook.json - 250+ Country Profiles

Use the `factbook` library for ready-to-use scripts for the world factbook (get open structured data e.g JSON etc.)


## What's the World Factbook?

The World Factbook [1][2] published by the Central Intelligence Agency (CIA)
offers free country profiles in the public domain (that is, no copyright(s), no rights reserved).

- [1] [The World Factbook](https://www.cia.gov/library/publications/the-world-factbook/)
- [2] [Wikipedia Article: The World Factbook](http://en.wikipedia.org/wiki/The_World_Factbook)


## Usage

### Get country profile page as a hash (that is, structured data e.g. nested key/values)

``` ruby
page = Factbook::Page.new( 'br' )   # br is the country code for Brazil
pp page.data                        # pretty print hash
```

resulting in:

``` ruby
{"Introduction"=>
  {"Background"=>
    {"text"=>
      "Following more than three centuries under Portuguese rule,
       Brazil gained its independence in 1822, ..."}},
 "Geography"=>
  {"Location"=>{"text"=>"Eastern South America, bordering the Atlantic Ocean"},
   "Geographic coordinates"=>{"text"=>"10 00 S, 55 00 W"},
   "Map references"=>{"text"=>"South America"},
   "Area"=>
    {"total"=>{"text"=>"8,515,770 sq km"},
     "land"=>{"text"=>"8,358,140 sq km"},
     "water"=>{"text"=>"157,630 sq km"},
     "note"=>
      {"text"=>
        "includes Arquipelago de Fernando de Noronha, Atol das Rocas, ..."}},
   "Area - comparative"=>
    {"text"=>"slightly smaller than the US"},
   "Land boundaries"=>
    {"total"=>{"text"=>"16,145 km"},
     "border countries (10)"=>
      {"text"=>
        "Argentina 1,263 km, Bolivia 3,403 km, Colombia 1,790 km,
        French Guiana 649 km, Guyana 1,308 km, Paraguay 1,371 km, Peru 2,659 km,
        Suriname 515 km, Uruguay 1,050 km, Venezuela 2,137 km"}},
   "Climate"=>{"text"=>"mostly tropical, but temperate in south"},
   "Elevation extremes"=>
    {"lowest point"=>{"text"=>"Atlantic Ocean 0 m"},
     "highest point"=>{"text"=>"Pico da Neblina 2,994 m"}},
   "Natural resources"=>
    {"text"=>
      "bauxite, gold, iron ore, manganese, nickel, phosphates, ..."},
    ...
```

### Use shortcut attribute accessors

``` ruby
pp page.background        ## same as page['Introduction']['Background']['text']
# => "Following more than three centuries..."
pp page.area              ## same as page['Geography'][''Area']['total']['text']
# => "8,515,770 sq km"
pp page.area_land         ## same as page['Geography'][''Area']['land']['text']
# => "8,358,140 sq km"
pp page.area_water        ## same as page['Geography'][''Area']['water']['text']
# => "157,630 sq km"
pp page.area_note         ## same as page['Geography'][''Area']['note']['text']
# => "includes Arquipelago de Fernando de Noronha, Atol das Rocas, ..."
pp page.area_comparative  ## same as page['Geography']['Area - comparative']['text']
# => "slightly smaller than the US"
pp page.climate           ## same as page['Geography']['Climate']['text']
# => "mostly tropical, but temperate in south"
pp page.terrain           ## same as page['Geography']['Terrain']['text']
# => "mostly flat to rolling lowlands in north; ..."
pp page.elevation_lowest  ## same as page['Geography']['Elevation extremes']['lowest point']['text']
# => "Atlantic Ocean 0 m"
pp page.elevation_highest ## same as page['Geography']['Elevation extremes']['highest point']['text']
# => "Pico da Neblina 2,994 m"
pp page.resources         ## same as page['Geography'][Natural resources']['text']
# => "bauxite, gold, iron ore, manganese, nickel, phosphates, ..."
...
```

See [`data/attributes.yml`](data/attributes.yml) for the full listing of all built-in attribute shortcut accessors.
See [Attributes](ATTRIBUTES.md) for a quick reference listing.


### Save to disk as JSON

``` ruby
page = Factbook::Page.new( 'br' )
File.open( 'br.json', 'w') do |f|
  f.write page.to_json
end
```


### List all codes

``` ruby
Factbook.codes.each do |code|
  pp code
end
```

resulting in:

``` ruby
#<struct Factbook::Codes::Code
 code="af",
 name="Afghanistan",
 category="Countries",
 region="South Asia">
#<struct Factbook::Codes::Code
 code="al",
 name="Albania",
 category="Countries",
 region="Europe">
#<struct Factbook::Codes::Code
 code="ag",
 name="Algeria",
 category="Countries",
 region="Africa">
#<struct Factbook::Codes::Code
 code="an",
 name="Andorra",
 category="Countries",
 region="Europe">
...
```

Note: You can filter codes by category e.g. Countries, Dependencies, Miscellaneous, Oceans, etc.
and/or by region e.g. Africa, Europe, South Asia, Central America and Caribbean, etc.


``` ruby

assert_equal 261, Factbook.codes.size

## categories
assert_equal 195, Factbook.codes.countries.size
assert_equal  52, Factbook.codes.dependencies.size
assert_equal   5, Factbook.codes.oceans.size
assert_equal   1, Factbook.codes.world.size
assert_equal   2, Factbook.codes.others.size
assert_equal   6, Factbook.codes.misc.size

## regions
assert_equal  55, Factbook.codes.europe.size
assert_equal   9, Factbook.codes.south_asia.size
assert_equal   6, Factbook.codes.central_asia.size
assert_equal  22, Factbook.codes.east_n_souteast_asia.size
assert_equal  19, Factbook.codes.middle_east.size
assert_equal  56, Factbook.codes.africa.size
assert_equal   7, Factbook.codes.north_america.size
assert_equal  33, Factbook.codes.central_america_n_caribbean.size
assert_equal  14, Factbook.codes.south_america.size
assert_equal  30, Factbook.codes.australia_oceania.size
assert_equal   4, Factbook.codes.antartica.size
assert_equal   5, Factbook.codes.region('Oceans').size
assert_equal   1, Factbook.codes.region('World').size

## categories + regions
assert_equal  45, Factbook.codes.countries.europe.size
...
```

See [`data/codes.csv`](data/codes.csv) for the built-in listing of all codes with categories and regions.



## The World Factbook Summary (267 Entries)

The World Factbook includes 267 entries -
195 sovereign countries /
2 others /
58 dependencies /
6 miscellaneous /
5 oceans /
1 world:


### Sovereign Countries (195)

**A**
`af` Afghanistan
`al` Albania
`ag` Algeria
`an` Andorra
`ao` Angola
`ac` Antigua and Barbuda
`ar` Argentina
`am` Armenia
`as` Australia
`au` Austria
`aj` Azerbaijan
**B**
`bf` The Bahamas
`ba` Bahrain
`bg` Bangladesh
`bb` Barbados
`bo` Belarus
`be` Belgium
`bh` Belize
`bn` Benin
`bt` Bhutan
`bl` Bolivia
`bk` Bosnia and Herzegovina
`bc` Botswana
`br` Brazil
`bx` Brunei
`bu` Bulgaria
`uv` Burkina Faso
`bm` Burma
`by` Burundi
**C**
`cb` Cambodia
`cm` Cameroon
`ca` Canada
`cv` Cape Verde
`ct` Central African Republic
`cd` Chad
`ci` Chile
`ch` China
`co` Colombia
`cn` Comoros
`cg` Congo DR
`cf` Congo
`cs` Costa Rica
`iv` Cote d'Ivoire
`hr` Croatia
`cu` Cuba
`cy` Cyprus
`ez` Czech Republic
**D**
`da` Denmark
`dj` Djibouti
`do` Dominica
`dr` Dominican Republic
**E**
`ec` Ecuador
`eg` Egypt
`es` El Salvador
`ek` Equatorial Guinea
`er` Eritrea
`en` Estonia
`et` Ethiopia
**F**
`fj` Fiji
`fi` Finland
`fr` France
**G**
`gb` Gabon
`ga` The Gambia
`gg` Georgia
`gm` Germany
`gh` Ghana
`gr` Greece
`gj` Grenada
`gt` Guatemala
`gv` Guinea
`pu` Guinea-Bissau
`gy` Guyana
**H**
`ha` Haiti
`ho` Honduras
`hu` Hungary
**I**
`ic` Iceland
`in` India
`id` Indonesia
`ir` Iran
`iz` Iraq
`ei` Ireland
`is` Israel
`it` Italy
**J**
`jm` Jamaica
`ja` Japan
`jo` Jordan
**K**
`kz` Kazakhstan
`ke` Kenya
`kr` Kiribati
`kn` North Korea
`ks` South Korea
`kv` Kosovo
`ku` Kuwait
`kg` Kyrgyzstan
**L**
`la` Laos
`lg` Latvia
`le` Lebanon
`lt` Lesotho
`li` Liberia
`ly` Libya
`ls` Liechtenstein
`lh` Lithuania
`lu` Luxembourg
**M**
`mk` Macedonia
`ma` Madagascar
`mi` Malawi
`my` Malaysia
`mv` Maldives
`ml` Mali
`mt` Malta
`rm` Marshall Islands
`mr` Mauritania
`mp` Mauritius
`mx` Mexico
`fm` Micronesia
`md` Moldova
`mn` Monaco
`mg` Mongolia
`mj` Montenegro
`mo` Morocco
`mz` Mozambique
**N**
`wa` Namibia
`nr` Nauru
`np` Nepal
`nl` Netherlands
`nz` New Zealand
`nu` Nicaragua
`ng` Niger
`ni` Nigeria
`no` Norway
**O**
`mu` Oman
**P**
`pk` Pakistan
`ps` Palau
`pm` Panama
`pp` Papua New Guinea
`pa` Paraguay
`pe` Peru
`rp` Philippines
`pl` Poland
`po` Portugal
**Q**
`qa` Qatar
**R**
`ro` Romania
`rs` Russia
`rw` Rwanda
**S**
`sc` Saint Kitts and Nevis
`st` Saint Lucia
`vc` Saint Vincent and the Grenadines
`ws` Samoa
`sm` San Marino
`tp` Sao Tome and Principe
`sa` Saudi Arabia
`sg` Senegal
`ri` Serbia
`se` Seychelles
`sl` Sierra Leone
`sn` Singapore
`lo` Slovakia
`si` Slovenia
`bp` Solomon Islands
`so` Somalia
`sf` South Africa
`od` South Sudan
`sp` Spain
`ce` Sri Lanka
`su` Sudan
`ns` Suriname
`wz` Swaziland
`sw` Sweden
`sz` Switzerland
`sy` Syria
**T**
`ti` Tajikistan
`tz` Tanzania
`th` Thailand
`tt` Timor-Leste
`to` Togo
`tn` Tonga
`td` Trinidad and Tobago
`ts` Tunisia
`tu` Turkey
`tx` Turkmenistan
`tv` Tuvalu
**U**
`ug` Uganda
`up` Ukraine
`ae` United Arab Emirates
`uk` United Kingdom
`us` United States
`uy` Uruguay
`uz` Uzbekistan
**V**
`nh` Vanuatu
`vt` Vatican City (Holy See)
`ve` Venezuela
`vm` Vietnam
**Y**
`ym` Yemen
**Z**
`za` Zambia
`zi` Zimbabwe


### Other (2)

`tw` Taiwan
`ee` European Union

### Dependencies (58)

Australia (6):
`at` Ashmore and Cartier Islands
`kt` Christmas Island
`ck` Cocos (Keeling) Islands
`cr` Coral Sea Islands
`hm` Heard Island and McDonald Islands
`nf` Norfolk Island

China (2):
`hk` Hong Kong
`mc` Macau

Denmark (2):
`fo` Faroe Islands
`gl` Greenland

France (8):
`ip` Clipperton Island
`fp` French Polynesia
`fs` French Southern and Antarctic Lands
`nc` New Caledonia
`tb` Saint Barthelemy
`rn` Saint Martin
`sb` Saint Pierre and Miquelon
`wf` Wallis and Futuna

Netherlands (3):
`aa` Aruba
`uc` Curacao
`nn` Sint Maarten

New Zealand (3):
`cw` Cook Islands
`ne` Niue
`tl` Tokelau

Norway (3):
`bv` Bouvet Island
`jn` Jan Mayen
`sv` Svalbard

Great Britain (17):
`ax` Akrotiri (Sovereign Base)
`av` Anguilla
`bd` Bermuda
`io` British Indian Ocean Territory
`vi` British Virgin Islands
`cj` Cayman Islands
`dx` Dhekelia (Sovereign Base)
`fk` Falkland Islands
`gi` Gibraltar
`gk` Guernsey
`je` Jersey
`im` Isle of Man
`mh` Montserrat
`pc` Pitcairn Islands
`sh` Saint Helena
`sx` South Georgia and the South Sandwich Islands
`tk` Turks and Caicos Islands

United States (14):
`aq` American Samoa
`gq` Guam
`bq` Navassa Island
`cq` Northern Mariana Islands
`rq` Puerto Rico
`vq` US Virgin Islands
`wq` Wake Island
`um` US Pacific Island Wildlife Refuges
(Baker Island, Howland Island, Jarvis Island, Johnston Atoll, Kingman Reef, Midway Islands, Palmyra Atoll)


### Miscellaneous (6)

`ay` Antarctica
`gz` Gaza Strip
`pf` Paracel Islands
`pg` Spratly Islands
`we` West Bank
`wi` Western Sahara

### Oceans (5)

`xq` Arctic Ocean
`zh` Atlantic Ocean
`xo` Indian Ocean
`zn` Pacific Ocean
`oo` Southern Ocean

### World (1)

`xx` World




## Ready-To-Use Public Domain Factbook Datasets

[opendatajson/factbook.json](https://github.com/opendatajson/factbook.json) - open (public domain)
factbook country profiles in JSON for all the world's countries (using internet domain names
for country codes e.g. Austria is `at.json` not `au.json`, Germany is `de.json` not `gm.json` and so on)


