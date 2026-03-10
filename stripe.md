# Configuration Stripe

## 1. Installer le CLI Stripe

```bash
brew install stripe/stripe-cli/stripe
```

## 2. Se connecter à son compte Stripe

```bash
stripe login
```

## 3. Créer le produit et le prix

```bash
stripe products create --name="Abonnement Mensuel" --description="Accès complet à l'application"
```

Copier le `id` du produit retourné (ex: `prod_XXXX`), puis :

```bash
stripe prices create \
  --product="prod_XXXX" \
  --unit-amount=990 \
  --currency=eur \
  --recurring[interval]=month
```

Copier le `id` du prix retourné (ex: `price_XXXX`) et le mettre dans `.env.local` :

```
STRIPE_PRICE_ID=price_XXXX
```

## 4. Récupérer la clé secrète

```bash
stripe config --list
```

Ou depuis le dashboard Stripe : **Developers > API keys > Secret key**

```
STRIPE_SECRET_KEY=sk_test_XXXX
```

## 5. Lancer le webhook en local

```bash
stripe listen --forward-to http://localhost:3000/api/stripe/webhook
```

Le CLI affiche un `webhook signing secret` (ex: `whsec_XXXX`). Le mettre dans `.env.local` :

```
STRIPE_WEBHOOK_SECRET=whsec_XXXX
```

## 6. Tester un paiement

Utiliser la carte de test Stripe : `4242 4242 4242 4242`, date future quelconque, CVC quelconque.

## Résumé des variables `.env.local`

```
STRIPE_SECRET_KEY=sk_test_XXXX
STRIPE_WEBHOOK_SECRET=whsec_XXXX
STRIPE_PRICE_ID=price_XXXX
NEXT_PUBLIC_APP_URL=http://localhost:3000
```
