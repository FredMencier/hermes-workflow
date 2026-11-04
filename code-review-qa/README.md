
     [ BACKLOG ] 
            │
            ▼ (Nouvelle tâche assignée)
 ┌────────────────────────────────────────────────────────┐
 │ 1. IN PROGRESS (Build)                                 │◄──────────────────┐
 │    ▶ Agent CODER                                       │                   │
 │    ▶ Action : Modifie les fichiers via l'outil 'fs'    │                   │
 └──────────────────────────┬─────────────────────────────┘                   │
                            │                                                 │
                            ▼ (Artefact : Fichier/Diff généré)                │
 ┌────────────────────────────────────────────────────────┐                   │
 │ 2. IN REVIEW                                           │                   │
 │    ▶ Agent REVIEWER                                    │                   │
 │    ▶ Action : Lit le code et inspecte le Diff          │                   │
 └──────────────────────────┬─────────────────────────────┘                   │
                            │                                                 │
            ┌───────────────┴───────────────┐                                 │
            │ Est-ce valide ?               │                                 │
            │                               │                                 │
            ├─► NON (Erreurs / Failles) ────┼─────────────────────────────────┤ (Retour au Coder
            │                               │                                  avec logs/rapport)
            └─► OUI ────────────────────────┐                                 │
                                            │                                 │
                                            ▼ (Validation du code)            │
 ┌────────────────────────────────────────────────────────┐                   │
 │ 3. IN QA (Testing)                                     │                   │
 │    ▶ Agent QA                                          │                   │
 │    ▶ Action : Exécute les scripts de test via 'bash'   │                   │
 └──────────────────────────┬─────────────────────────────┘                   │
                            │                                                 │
            ┌───────────────┴───────────────┐                                 │
            │ Les tests passent-ils ?       │                                 │
            │                               │                                 │
            ├─► NON (Linter/Tests échoués) ─┼─────────────────────────────────┘
            │                               │
            └─► OUI (Code de retour 0) ─────┐
                                            │
                                            ▼ (Succès total)
       [ 4. DONE ] ───► L'Orchestrateur clôture la tâche et archive les logs
