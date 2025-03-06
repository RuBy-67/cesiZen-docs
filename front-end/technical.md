# 🛠️ Documentation Technique Frontend

## 🏗️ Architecture

### 📦 Structure du Projet
```
frontend/
├── src/
│   ├── app/                 # Core de l'application
│   │   ├── components/      # Composants réutilisables
│   │   ├── pages/          # Pages de l'application
│   │   ├── services/       # Services et logique métier
│   │   ├── models/         # Interfaces et types
│   │   └── shared/         # Ressources partagées
│   ├── assets/             # Ressources statiques
│   ├── environments/       # Configuration par environnement
│   └── theme/             # Styles globaux et thèmes
└── ...
```

### 🔄 Flux de Données
1. **State Management**
   - Utilisation de NgRx pour la gestion d'état
   - Actions et reducers par fonctionnalité
   - Selectors pour l'accès aux données
   - Effects pour les opérations asynchrones

2. **Communication API**
   - Services HTTP centralisés
   - Intercepteurs pour les headers
   - Gestion des erreurs globale
   - Cache des requêtes

## 🎨 Design System

### 🎯 Composants Core
1. **Layout**
   ```typescript
   @Component({
     selector: 'app-layout',
     template: `
       <ion-app>
         <ion-header>...</ion-header>
         <ion-content>
           <ng-content></ng-content>
         </ion-content>
       </ion-app>
     `
   })
   ```

2. **Cards**
   ```typescript
   @Component({
     selector: 'app-emotion-card',
     template: `
       <ion-card [class]="darkMode ? 'dark' : 'light'">
         <ion-card-header>...</ion-card-header>
         <ion-card-content>...</ion-card-content>
       </ion-card>
     `
   })
   ```

### 🎨 Thèmes
1. **Variables CSS**
   ```scss
   :root {
     --primary: #4A90E2;
     --secondary: #50E3C2;
     --background: #F5F5F5;
     --text: #333333;
     
     .dark-theme {
       --background: #1A1A1A;
       --text: #FFFFFF;
     }
   }
   ```

2. **Utilities**
   ```scss
   .flex-center {
     display: flex;
     align-items: center;
     justify-content: center;
   }
   ```

## 🔧 Configuration

### 📡 Environment
```typescript
// environment.ts
export const environment = {
  production: false,
  apiUrl: 'http://localhost:3000/api',
  version: '1.0.0',
  features: {
    darkMode: true,
    notifications: true
  }
};
```

### 🔒 Sécurité
```typescript
// auth.interceptor.ts
@Injectable()
export class AuthInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler) {
    const token = localStorage.getItem('token');
    if (token) {
      req = req.clone({
        headers: req.headers.set('Authorization', `Bearer ${token}`)
      });
    }
    return next.handle(req);
  }
}
```

## 📱 Responsive Design

### 📐 Breakpoints
```scss
$breakpoints: (
  'mobile': 320px,
  'tablet': 768px,
  'desktop': 1024px,
  'wide': 1440px
);

@mixin respond-to($breakpoint) {
  @media (min-width: map-get($breakpoints, $breakpoint)) {
    @content;
  }
}
```

### 🖥️ Layouts Adaptatifs
```typescript
@Component({
  template: `
    <div [class]="isMobile ? 'mobile-layout' : 'desktop-layout'">
      <ng-content></ng-content>
    </div>
  `
})
export class ResponsiveLayoutComponent {
  isMobile = window.innerWidth < 768;
}
```

## 🚀 Performance

### ⚡ Optimisations
1. **Lazy Loading**
   ```typescript
   const routes: Routes = [
     {
       path: 'dashboard',
       loadChildren: () => import('./pages/dashboard/dashboard.module')
         .then(m => m.DashboardModule)
     }
   ];
   ```

2. **Mémoire**
   ```typescript
   @Component({
     changeDetection: ChangeDetectionStrategy.OnPush
   })
   ```

### 📊 Monitoring
- Integration de Google Analytics
- Tracking des performances
- Logs d'erreurs
- Métriques utilisateur

## 🧪 Tests

### 🎯 Unit Tests
```typescript
describe('EmotionTrackerComponent', () => {
  let component: EmotionTrackerComponent;
  let fixture: ComponentFixture<EmotionTrackerComponent>;

  beforeEach(async () => {
    await TestBed.configureTestingModule({
      declarations: [ EmotionTrackerComponent ],
      imports: [ IonicModule.forRoot() ]
    }).compileComponents();
  });

  it('should create', () => {
    expect(component).toBeTruthy();
  });
});
```

### 🤖 E2E Tests
```typescript
describe('Emotion Tracker', () => {
  it('should add new emotion', () => {
    cy.visit('/tracker');
    cy.get('[data-test="emotion-select"]').click();
    cy.get('[data-test="emotion-joy"]').click();
    cy.get('[data-test="save-button"]').click();
    cy.get('[data-test="success-message"]').should('be.visible');
  });
});
```

## 📦 Build et Déploiement

### 🔨 Scripts
```json
{
  "scripts": {
    "start": "ng serve",
    "build": "ng build --configuration production",
    "test": "ng test",
    "lint": "ng lint",
    "e2e": "cypress run"
  }
}
```

### 🚀 CI/CD
```yaml
name: Frontend CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Setup Node.js
        uses: actions/setup-node@v2
      - name: Install dependencies
        run: npm ci
      - name: Run tests
        run: npm test
      - name: Build
        run: npm run build
```

## 📚 Bonnes Pratiques

### 🎯 Code Style
- Utilisation de ESLint et Prettier
- Conventions de nommage cohérentes
- Documentation des composants
- Types stricts TypeScript

### 🔄 State Management
- Actions typées
- Selectors mémorisés
- Effects isolés
- Tests des reducers

### 🎨 UI/UX
- Composants atomiques
- Styles modulaires
- Accessibilité (WCAG)
- Support i18n 