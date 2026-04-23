# projeto-abstract-factory

    // Produtos Abstratos
    interface Motor {
        String cilindradas();
    }

    interface Interior {
        String material();
    }

// Abstract Factory
    interface CarFactory {
        Motor criarMotor();
        Interior criarInterior();
    }

// Implementações: Luxo
    class LuxoMotor implements Motor {
        public String cilindradas() { return "V8 4.0L"; }
    }

    class LuxoInterior implements Interior {
        public String material() { return "Couro Napa"; }
    }

    class LuxoCarFactory implements CarFactory {
        public Motor criarMotor() { return new LuxoMotor(); }
        public Interior criarInterior() { return new LuxoInterior(); }
    }

// Implementações: Econômico
    class EconomicoMotor implements Motor {
        public String cilindradas() { return "1.0 Flex"; }
    }

    class EconomicoInterior implements Interior {
        public String material() { return "Tecido padrão"; }
    }

    class EconomicoCarFactory implements CarFactory {
        public Motor criarMotor() { return new EconomicoMotor(); }
        public Interior criarInterior() { return new EconomicoInterior(); }
    }

// Cliente
    class LinhaDeMontagem {
        private final CarFactory factory;

        public LinhaDeMontagem(CarFactory factory) {
            this.factory = factory;
        }

        public String montarCarro() {
            Motor motor = factory.criarMotor();
            Interior interior = factory.criarInterior();

            return String.format("Motor: %s | Interior: %s",
                    motor.cilindradas(), interior.material());
        }
    }

//Classe Principal para Execução
    public class Main {
        public static void main(String[] args) {
            LinhaDeMontagem linhaLuxo = new LinhaDeMontagem(new LuxoCarFactory());
            LinhaDeMontagem linhaEco = new LinhaDeMontagem(new EconomicoCarFactory());

            System.out.println("Carro Luxo -> " + linhaLuxo.montarCarro());
            System.out.println("Carro Eco  -> " + linhaEco.montarCarro());
        }
    }



