# Guide de démarrage — Passeport de Compétences MSDMC

## Projet Supabase créé
- **URL :** `https://tbpucspbkmjmqzhloopd.supabase.co`
- **Région :** eu-west-3 (Paris)
- Le schéma (tables + RLS) est déjà appliqué.

---

## 1. Créer le premier compte Admin

Dans [Supabase Dashboard → Authentication → Users](https://supabase.com/dashboard/project/tbpucspbkmjmqzhloopd/auth/users) :

1. Cliquer **Add user → Create new user**
2. Renseigner ton email + un mot de passe temporaire
3. Cocher **Auto Confirm User**
4. Cliquer **Create User**

Ensuite, dans **Table Editor → profiles**, trouver la ligne créée et mettre `role = admin`.

---

## 2. Créer des comptes formateurs

Même procédure, mais `role = teacher`.

---

## 3. Importer les apprenants en masse

### Option A — Via l'interface Admin de l'app
1. Connecte-toi avec ton compte admin
2. Menu **Import CSV / Excel**
3. Prépare ton fichier au format :
```
email,prenom,nom,campus,promo,role
jean.dupont@ecole.fr,Jean,Dupont,Mulhouse,2026,student
```
4. Glisse le fichier → aperçu → **Importer**

### Option B — Via Supabase Dashboard directement
Dans Authentication → Users, importer via l'API ou le dashboard.

---

## 4. Activer les e-mails d'invitation (optionnel)

Dans **Authentication → Email Templates**, personnalise les e-mails envoyés aux nouveaux utilisateurs (invitation, reset mot de passe).

Pour que les apprenants reçoivent un lien de connexion automatique :
- Utiliser **Authentication → Users → Invite** plutôt que Create
- L'apprenant reçoit un lien magic-link pour définir son mot de passe

---

## 5. Déployer l'application

### Option A — Ouvrir localement
Double-cliquer sur `passeport.html` → s'ouvre dans le navigateur, fonctionnel immédiatement.

### Option B — Netlify Drop (gratuit, 30 secondes)
1. Aller sur [drop.netlify.com](https://drop.netlify.com)
2. Glisser le fichier `passeport.html`
3. Partager l'URL générée avec tes apprenants

### Option C — GitHub Pages
Pousser `passeport.html` dans un repo GitHub → activer Pages → URL stable.

---

## Structure de la base de données

| Table | Description |
|-------|-------------|
| `profiles` | Profils liés aux comptes auth (nom, rôle, campus, promo) |
| `competency_progress` | Coches + niveaux + commentaires par apprenant |
| `teacher_notes` | Notes des formateurs sur les apprenants |

---

## Rôles

| Rôle | Accès |
|------|-------|
| `student` | Son passeport uniquement (cocher, commenter, voir sa progression) |
| `teacher` | Tous les apprenants + notes formateur |
| `admin` | Tout + import CSV + gestion utilisateurs |

---

## Fonctionnalités de l'app

**Apprenant**
- ✅ Cocher les 35 compétences réparties en 5 blocs RNCP
- ⭐ Évaluer son niveau (1 à 3 étoiles par compétence)
- 💬 Ajouter un commentaire / preuve par compétence
- 📊 Vue progression par bloc

**Formateur**
- 👥 Tableau de bord avec progression de chaque apprenant
- 📋 Fiche détaillée : compétences cochées + niveaux + commentaires
- 📝 Notes formateur par apprenant

**Admin**
- 📥 Import CSV/Excel des apprenants
- 👤 Vue de tous les utilisateurs
- ⚙️ Création de comptes

---

## Évolutions possibles
- Export PDF du passeport (impression / certificat)
- Notifications e-mail aux formateurs quand un bloc est complété
- Validation formateur d'une compétence cochée par l'apprenant
- Tableau comparatif inter-promotions
