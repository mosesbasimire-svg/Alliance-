SITE HOMMAGE AMESHINDA — PUBLICATION IMMÉDIATE

Cette version publie immédiatement les hommages envoyés. Tous les visiteurs peuvent lire les messages approuvés automatiquement (statut approuve).

IMPORTANT : dans Supabase > SQL Editor, exécute cette migration une seule fois pour remplacer les anciennes règles de validation :

DROP POLICY IF EXISTS "Lire les hommages approuves" ON public.hommages;
DROP POLICY IF EXISTS "Envoyer un hommage" ON public.hommages;

CREATE POLICY "Lire tous les hommages publics"
ON public.hommages FOR SELECT TO anon, authenticated
USING (true);

CREATE POLICY "Publier directement un hommage"
ON public.hommages FOR INSERT TO anon, authenticated
WITH CHECK (statut = 'approuve');

La politique de stockage des photos reste inchangée.

SÉCURITÉ : ne jamais mettre une clé sb_secret ou service_role dans le site. Le site utilise uniquement la clé sb_publishable.

Pour publier : remplace le fichier index.html du dépôt GitHub par celui de ce ZIP, puis exécute la migration SQL ci-dessus dans Supabase.
