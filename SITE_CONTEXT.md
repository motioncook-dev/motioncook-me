# motioncook.me — Direction Artistique & Technique

## Identité
- **Nom** : motioncook.me
- **Artiste** : Stéphane Daguin
- **Localisation** : Madrid, Espagne
- **Rôle** : Senior Houdini Artist · FX Technical Director
- **Expérience** : 15+ ans en publicité, séries et cinéma

## Direction Artistique
- **Style** : Dark mode minimaliste, accent orange (#ff4d00)
- **Couleurs** : Fond noir profond (#0a0a0a), cartes sombres (#1a1a1a), texte blanc cassé (#f0f0f0)
- **Typographie** : Outfit + Space Mono
- **Ambiance** : Cinématique, industrielle, premium
- **Layout** : 3 colonnes (Expérience | Vidéos | Formation)
- **Tool logos** : 3 logos (Houdini, Nuke, ComfyUI)

## Direction Technique
### Fonctionnalités
1. **Multilingue** : FR (par défaut), EN, ES via `setLanguage()` + `[data-i18n]`
   - Clés i18n actuelles : `hero.badge`, `hero.description`, `hero.cta`, `share.button`, `footer.copyright`, `page.title`, `scroll`, `filter.*`, `cv.lang.*`
2. **Tool logos** : grays → color on click → texte descriptif dans la langue courante
3. **Projets** : Filtres (Film | Pub | Animation 3D)
4. **Vidéos** : Thumbnails avec lecture inline
5. **Formation** : Certificats + diplômes

### Code actuel (`6ba23dd`)
- `document.documentElement.lang` = source de vérité pour la langue courante
- `getOriginalDesc()` = `translations[lang]['hero.description']` (dynamique)
- `classList.toggle('active')` pour logos
- `e.preventDefault()` sur click + document click
- `document.addEventListener('click', ...)` exclut `.lang-btn` et `.tool-logo-wrapper`
- CSS `.tool-logo-wrapper.active .tool-logo { filter: grayscale(0%); }`

### Bugs connus
- Houdini logo : parfois le clic ne fonctionne pas correctement sur mobile
- `e.preventDefault()` sur click peut bloquer le mobile
- `document.documentElement.lang` comme vérité fonctionne bien pour le texte

### Déploiement
- GitHub Pages main = `6ba23dd`
- Backup branch = `backup-working` = `6ba23dd`
- Cron jobs : uptime + audit liens

### Notes de développement
- **Outil `patch` non fiable** : `patch` échoue silencieusement sur les remplacements multi-lignes dans index.html. Utiliser Python (`execute_code` avec `content.replace()`) à la place. Toujours vérifier avec `grep` après.
- Le serveur HTTP (port 8080) meurt souvent — toujours relancer avec `pkill` + `nohup`
- Ne pas utiliser `pointerup` ou `touchend` seuls → double-fire
- Ne pas utiliser `handleLogoTap` avec `pointerup` → casse Houdini
- `e.preventDefault()` sur `click` marche sur desktop mais peut bloquer mobile
- `document.documentElement.lang` est fiable pour la langue courante
