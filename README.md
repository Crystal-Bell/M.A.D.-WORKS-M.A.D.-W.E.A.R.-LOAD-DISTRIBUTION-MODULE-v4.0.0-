// ============================================================================
// M.A.D. WORKS: M.A.D. W.E.A.R. LOAD-DISTRIBUTION MODULE (v4.0.0)
// Passive Ergonomic Strain Minimization & Modular Utility Telemetry
// ============================================================================

use std::collections::HashMap;

#[derive(Debug, Clone)]
pub struct UtilityModuleSpec {
    pub module_name: String,
    pub weight_kg: f64,
    pub load_capacity_limit_kg: f64,
    pub thermal_shielding_active: bool,
}

pub struct MadWearEngine {
    modules: HashMap<String, UtilityModuleSpec>,
}

impl MadWearEngine {
    pub fn new() -> Self {
        Self {
            modules: HashMap::new(),
        }
    }

    pub fn attach_utility_module(&mut self, spec: UtilityModuleSpec) {
        println!("[M.A.D. W.E.A.R.] Equipping modular utility component: {} ({} kg)", spec.module_name, spec.weight_kg);
        self.modules.insert(spec.module_name.clone(), spec);
    }

    pub fn audit_load_distribution(&self, max_allowable_load_kg: f64) -> bool {
        let total_weight: f64 = self.modules.values().map(|m| m.weight_kg).sum();
        
        if total_weight > max_allowable_load_kg {
            eprintln!("[LOAD WARNING] Total utility weight {} kg exceeds ergonomic threshold of {} kg.", total_weight, max_allowable_load_kg);
            false
        } else {
            println!("[ERGONOMIC PASS] Total utility weight {} kg is safely within operating limits.", total_weight);
            true
        }
    }
}

fn main() {
    let mut wear_engine = MadWearEngine::new();

    wear_engine.attach_utility_module(UtilityModuleSpec {
        module_name: "M.A.D. Grips+ Thermal Shell".to_string(),
        weight_kg: 1.2,
        load_capacity_limit_kg: 15.0,
        thermal_shielding_active: true,
    });

    wear_engine.attach_utility_module(UtilityModuleSpec {
        module_name: "M.A.D. Suite Seat Deployment Harness".to_string(),
        weight_kg: 3.4,
        load_capacity_limit_kg: 50.0,
        thermal_shielding_active: false,
    });

    if wear_engine.audit_load_distribution(10.0) {
        println!("Modular apparel framework successfully verified for operational deployment.");
    }
}
# M.A.D.-WORKS-M.A.D.-W.E.A.R.-LOAD-DISTRIBUTION-MODULE-v4.0.0-