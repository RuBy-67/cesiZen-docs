# 🧪 Tests Unitaires Frontend - Cersizen

## 📋 Structure des Tests

### 📁 Organisation des Fichiers
```
src/
├── app/
│   ├── components/
│   │   ├── __tests__/
│   │   │   ├── emotion-card.component.spec.ts
│   │   │   ├── breathing-timer.component.spec.ts
│   │   │   └── ...
│   ├── services/
│   │   ├── __tests__/
│   │   │   ├── auth.service.spec.ts
│   │   │   ├── emotion.service.spec.ts
│   │   │   └── ...
│   └── store/
       ├── __tests__/
           ├── auth.reducer.spec.ts
           ├── emotion.effects.spec.ts
           └── ...
```

## 🧪 Tests des Composants

### 1. Composant EmotionCard
```typescript
// emotion-card.component.spec.ts
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { EmotionCardComponent } from '../emotion-card.component';

describe('EmotionCardComponent', () => {
  let component: EmotionCardComponent;
  let fixture: ComponentFixture<EmotionCardComponent>;

  beforeEach(async () => {
    await TestBed.configureTestingModule({
      declarations: [ EmotionCardComponent ],
      imports: [ IonicModule.forRoot() ]
    }).compileComponents();

    fixture = TestBed.createComponent(EmotionCardComponent);
    component = fixture.componentInstance;
  });

  it('devrait créer le composant', () => {
    expect(component).toBeTruthy();
  });

  it('devrait afficher le nom de l\'émotion', () => {
    component.emotion = { id: 1, name: 'Joie', baseId: 1 };
    fixture.detectChanges();
    const compiled = fixture.nativeElement;
    expect(compiled.querySelector('.emotion-name').textContent).toContain('Joie');
  });

  it('devrait émettre l\'événement de sélection', () => {
    const spy = jest.spyOn(component.selected, 'emit');
    component.onSelect();
    expect(spy).toHaveBeenCalled();
  });
});
```

### 2. Composant BreathingTimer
```typescript
// breathing-timer.component.spec.ts
describe('BreathingTimerComponent', () => {
  let component: BreathingTimerComponent;
  let fixture: ComponentFixture<BreathingTimerComponent>;

  beforeEach(async () => {
    await TestBed.configureTestingModule({
      declarations: [ BreathingTimerComponent ]
    }).compileComponents();
  });

  it('devrait démarrer le minuteur', fakeAsync(() => {
    component.duration = 5;
    component.start();
    tick(1000);
    expect(component.timeLeft).toBe(4);
    tick(4000);
    expect(component.timeLeft).toBe(0);
  }));

  it('devrait mettre en pause le minuteur', () => {
    component.start();
    component.pause();
    expect(component.isPaused).toBeTruthy();
  });
});
```

## 🔧 Tests des Services

### 1. Service d'Authentification
```typescript
// auth.service.spec.ts
describe('AuthService', () => {
  let service: AuthService;
  let httpMock: HttpTestingController;

  beforeEach(() => {
    TestBed.configureTestingModule({
      imports: [ HttpClientTestingModule ],
      providers: [ AuthService ]
    });
    service = TestBed.inject(AuthService);
    httpMock = TestBed.inject(HttpTestingController);
  });

  it('devrait authentifier l\'utilisateur', () => {
    const credentials = {
      email: 'test@test.com',
      password: 'password123'
    };

    service.login(credentials).subscribe(response => {
      expect(response.token).toBeTruthy();
    });

    const req = httpMock.expectOne('/api/auth/login');
    expect(req.request.method).toBe('POST');
    req.flush({ token: 'fake-jwt-token' });
  });
});
```

### 2. Service des Émotions
```typescript
// emotion.service.spec.ts
describe('EmotionService', () => {
  let service: EmotionService;
  let httpMock: HttpTestingController;

  beforeEach(() => {
    TestBed.configureTestingModule({
      imports: [ HttpClientTestingModule ],
      providers: [ EmotionService ]
    });
  });

  it('devrait récupérer la liste des émotions', () => {
    service.getEmotions().subscribe(emotions => {
      expect(emotions.length).toBe(2);
      expect(emotions[0].name).toBe('Joie');
    });

    const req = httpMock.expectOne('/api/emotions');
    req.flush([
      { id: 1, name: 'Joie', baseId: 1 },
      { id: 2, name: 'Tristesse', baseId: 2 }
    ]);
  });
});
```

## 📊 Tests du Store (NgRx)

### 1. Tests des Reducers
```typescript
// auth.reducer.spec.ts
describe('Auth Reducer', () => {
  it('devrait mettre à jour l\'état après login', () => {
    const initialState = { user: null, token: null };
    const action = login({ user: mockUser, token: 'token' });
    const state = authReducer(initialState, action);

    expect(state.user).toEqual(mockUser);
    expect(state.token).toBe('token');
  });

  it('devrait réinitialiser l\'état après logout', () => {
    const state = authReducer(
      { user: mockUser, token: 'token' },
      logout()
    );

    expect(state).toEqual({ user: null, token: null });
  });
});
```

### 2. Tests des Effects
```typescript
// emotion.effects.spec.ts
describe('Emotion Effects', () => {
  let effects: EmotionEffects;
  let actions$: Observable<any>;
  let emotionService: EmotionService;

  beforeEach(() => {
    TestBed.configureTestingModule({
      providers: [
        EmotionEffects,
        provideMockActions(() => actions$),
        {
          provide: EmotionService,
          useValue: { getEmotions: jest.fn() }
        }
      ]
    });

    effects = TestBed.inject(EmotionEffects);
    emotionService = TestBed.inject(EmotionService);
  });

  it('devrait charger les émotions', () => {
    const emotions = [
      { id: 1, name: 'Joie', baseId: 1 }
    ];

    actions$ = hot('-a', { a: loadEmotions() });
    const response = cold('-a|', { a: emotions });
    emotionService.getEmotions = jest.fn(() => response);

    const expected = hot('--b', {
      b: loadEmotionsSuccess({ emotions })
    });

    expect(effects.loadEmotions$).toBeObservable(expected);
  });
});
```

## 🛠️ Configuration des Tests

### 1. Jest Configuration
```javascript
// jest.config.js
module.exports = {
  preset: 'jest-preset-angular',
  setupFilesAfterEnv: ['<rootDir>/setup-jest.ts'],
  testPathIgnorePatterns: [
    '<rootDir>/node_modules/',
    '<rootDir>/dist/'
  ],
  coverageDirectory: 'coverage/frontend',
  coverageReporters: ['html', 'lcov', 'text'],
  coverageThreshold: {
    global: {
      branches: 80,
      functions: 80,
      lines: 80,
      statements: 80
    }
  }
};
```

### 2. Scripts de Test
```json
{
  "scripts": {
    "test": "jest",
    "test:watch": "jest --watch",
    "test:coverage": "jest --coverage",
    "test:debug": "node --inspect-brk jest --runInBand"
  }
}
```

## 📈 Métriques et Rapports

### 1. Couverture de Code
- **Composants** : > 85%
- **Services** : > 90%
- **Store** : > 90%
- **Utils** : 100%

### 2. Format du Rapport
```markdown
# Rapport de Tests Unitaires
Date: YYYY-MM-DD

## Résumé
- Total Tests: XX
- Réussis: XX
- Échecs: XX
- Couverture: XX%

## Détails par Module
1. Composants: XX%
2. Services: XX%
3. Store: XX%
4. Utils: XX%

## Points d'Attention
- [Liste des zones nécessitant plus de tests]
- [Composants complexes à tester]
```

## 🔍 Bonnes Pratiques

### 1. Organisation des Tests
- Un fichier de test par composant/service
- Nommage clair et descriptif des tests
- Regroupement logique des tests similaires
- Isolation des tests

### 2. Assertions
- Tests positifs et négatifs
- Vérification des cas limites
- Tests des effets de bord
- Validation des événements émis

### 3. Mocks et Stubs
- Création de mocks réutilisables
- Simulation des dépendances externes
- Isolation du code testé
- Contrôle des scénarios de test 
