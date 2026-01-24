# 🏛️ Arhitectura Ecosistemului AMD Validation

Acest document descrie modul în care componentele de Python, Java și Prometheus conlucrează pentru a forma un pipeline de validare și monitorizare de nivel Enterprise.

## 🔄 Fluxul Datelor (The Data Pipeline)

1. **Orchestrarea (Python)**: 
   - Fișier: `run_validation.py`
   - Rol: Este "Creierul" sistemului. Rulează logica de business, generează dovezi de integritate (SHA-256) și acționează ca un pod între componente.
   - Output: Actualizează periodic fișierul de metrici în `data/vault/metrics.txt`.

2. **Monitorizarea (Prometheus)**:
   - Fișier: `prometheus.yml`
   - Rol: "Ochiul" sistemului. Scanează fișierul de metrici la fiecare 15 secunde folosind mecanismul `file_sd_configs`.
   - Rezultat: Transformă datele brute în grafice de performanță și alerte de uptime.

3. **Validarea Codului (Java/JUnit)**:
   - Cale Producție: `src/test/java/com/adrianroman/btp/unit/`
   - Rol: Garantează că regulile de securitate sunt respectate la nivel de unitate de cod (Unit Testing) înainte ca sistemul să fie lansat.

4. **Testarea de Stres (JMeter)**:
   - Cale Producție: `tests/jmeter/`
   - Rol: Simulează utilizatori reali pentru a verifica reziliența infrastructurii sub sarcină.

---

## 🛠️ Căile de Producție (Production Paths)

| Componentă | Locație în Producție | Tehnologie |
| :--- | :--- | :--- |
| **Main Engine** | `./run_validation.py` | Python 3.x |
| **Java Unit Tests** | `./src/test/java/com/adrianroman/btp/unit/` | JUnit 5 |
| **Performance** | `./tests/jmeter/` | Apache JMeter |
| **Monitoring Config** | `./prometheus.yml` | YAML / Prometheus |
| **Data Vault** | `./data/vault/` | Secure Storage |

---

## 🚀 Mesaj Strategic
Acest proiect demonstrează o abordare **DevSecOps Hybrid**. Prin combinarea Python (agilitate) cu Java (stabilitate Enterprise) și Prometheus (vizibilitate), am creat un cadru tehnic unde "Adevărul tehnic este fundamentul respectului".
