import java.util.Arrays;

public class GoldPricePrediction {
    // Simple linear regression model parameters
    private double slope;
    private double intercept;

    public void train(double[] x, double[] y) {
        // Calculate mean of x and y
        double xMean = Arrays.stream(x).average().orElse(0);
        double yMean = Arrays.stream(y).average().orElse(0);

        // Calculate slope
        double numerator = 0;
        double denominator = 0;
        for (int i = 0; i < x.length; i++) {
            numerator += (x[i] - xMean) * (y[i] - yMean);
            denominator += Math.pow(x[i] - xMean, 2);
        }
        slope = numerator / denominator;

        // Calculate intercept
        intercept = yMean - slope * xMean;
    }

    public double predict(double x) {
        return slope * x + intercept;
    }

    public static void main(String[] args) {
        // Example data
        double[] historicalYears = {2015, 2016, 2017, 2018, 2019};
        double[] goldPrices = {1200, 1250, 1300, 1350, 1400}; // In USD per ounce

        // Initialize and train the model
        GoldPricePrediction model = new GoldPricePrediction();
        model.train(historicalYears, goldPrices);

        // Predict future price for the year 2020
        double futureYear = 2020;
        double predictedPrice = model.predict(futureYear);
        System.out.println("Predicted gold price for " + futureYear + ": $" + predictedPrice);
    }
}
