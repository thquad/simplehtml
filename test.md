# 2020-11-18 Stratos theme

- Topic: Wieso läd das example theme nicht?

  - Frage: Was passiert wenn ich nur `npm start` mache?

    - Nur ein Frontend startet!
    - Was macht `npm start` genau?
      - `ng serve`
      - Info: Ich muss `npm run start` machen um das `start` aus dem scripts object zu starten.

  - Frage: Was passiert bei `npm run start-dev`?

    - Ich seh kein Unterschied.

  - Info: Das manuell hinzugefügte Extension wird geladen. Siehe (^1)

  - stratos.yaml

    - Info: Die includes in stratos.yaml sollte das theme eigentlich wieder hinzufügen. Die sind default disabled. Beim build werden die nicht durch die stratos.yaml hinzugefügt.
    - Frage: Wo werden die disabled? (Lösung ist wahrscheinlich nicht hier, aber etwas was man mal recherchieren könnte.)
      - -
    - Info: In der doc steht, dass die `stratos.yaml` im root hinzugefügt werden soll. In `./` wirft ein `npm start` aber Error (^2). Im `./src/` Ordner scheint aber nichts geändert zu werden.

  - Hypothesis: Wenn die Ordner automatisch exluded sind, aber jedes Theme automatisch included wird, muss ich dann nicht nur die Ordner umbennen?

    - Frage: Was passiert wenn ich den Ordner umbenenne? 

      - Kopieren und umbennen an sich macht nichts.

    - Frage: Ordner umbennen und pfade anpassen.

      - example-extensions-copy erstellt

      - `tsconfig.json` pfad für `@example/extensions` angepasst an copy ordner.

      - Ich merke gerade das es nichts ändern wird, da nicht der pfad exluded ist, sondern das @. Antwort: Ja, hat nichts gemacht.

      - @example/extensions umbennen und im code anpassen? Neuer Name @acmeexample/extensions

        - > L1 Beim build wurde die extension hinzugefügt.  Das es tatsächlich funktioniert hat, sieht man an dem "Example App Tab", welches hinzugefügt wurde wenn man eine Application anschaut.

  - Info: Ich habe gerade gemerkt, dass im `example-theme` in der `"name"` property ein `"@example/theme"` erwähnt wird, dass aber nicht in der `tsconfig.json` als path angegeben ist.

    - Frage: Was passiert wenn ich den path hinzufüge? 
      - Nichts.

^1

```
Packages:
 + @stratosui/cf-autoscaler
 + @stratosui/cloud-foundry
 + @stratosui/core
 + @stratosui/kubernetes
 + @myexamples/extensions
 + @stratosui/shared
 + @stratosui/theme
Using theme @stratosui/theme
Building with these extensions:
 + @stratosui/cf-autoscaler
 + @stratosui/cloud-foundry
 + @stratosui/kubernetes
 + @myexamples/extensions
```

^2

```
An unhandled exception occurred: Cannot read property 'forEach' of undefined
See "/tmp/ng-RV8Xnq/angular-errors.log" for further details.
```

