---
layout: post
title: Import von csv-Dateien
subtitle: Die TextFieldParser-Klasse
cover-img: /assets/img/graybg.png
thumbnail-img: /assets/img/cshard.png
share-img: /assets/img/start.jpg
tags: [c#, csv, TextFieldParser ]
author: Oliver Kocks
---

Der Import von csv-Dateien ist ein recht typisches Problem. Glücklicherweise bietet c# hier (etwas versteckt) in der TextFieldParser-Klasse die notwendige Funktionalität. Dies hat den Vorteil, dass man sich
nicht selbst um einige der Randprobleme kümmern muss (unvollständige Zeilen, leere Zeilen, umgeschlüsselte Trennzeichen etc.).

Beispiel:

```

using Microsoft.VisualBasic.FileIO;

...

try
{
	using ( TextReader textReader = new StringReader( csvString ) )
    using ( TextFieldParser textFieldParser = new( textReader ) )
    {
		parser.SetDelimiters( delimiterChar );
        while ( !textFieldParser.EndOfData )
        {
			String[]? csvData = textFieldParser.ReadFields();
            if ( csvData != null )
				...
		}
	}
}
catch ( Exception e ) 
{
	...
}

```
         
Als Ergebnis erhält man ein pro ReadFields-Aufruf ein Array der Spaltenwerte, die man entsprechend verarbeiten kann.
Von dem "VisualBasic"-Namespace muss man sich nicht abschrecken lassen. Die Klasse ist in einer der Standard-dotnet-Bibliotheken eingebunden, der exotische Namespace wahrscheinlich ein Relikt aus den
dotnet-Anfangszeiten.		 


