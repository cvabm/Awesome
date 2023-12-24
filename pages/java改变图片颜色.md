```java
import java.awt.Color;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

import javax.imageio.ImageIO;

class changeImgColor {
    public static void main(String[] args) {
        String input = "e:/test/test.png";
        String output = "e:/test/output.png";
        String color = "#ffffff";
        try {
            BufferedImage image = ImageIO.read(new File(input));
            BufferedImage modifyColorWithoutChangingTransparency = modifyColorWithoutChangingTransparency(image, color);
            ImageIO.write(modifyColorWithoutChangingTransparency, "png", new File(output));
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static BufferedImage modifyColorWithoutChangingTransparency(BufferedImage originalImage, String hexColor) {
        int width = originalImage.getWidth();
        int height = originalImage.getHeight();
        BufferedImage modifiedImage = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
        for (int i = 0; i < width; i++) {
            for (int j = 0; j < height; j++) {
                int originalRGB = originalImage.getRGB(i, j);
                Color originalColor = new Color(originalRGB, true);
                Color color = Color.decode(hexColor);
                int red = color.getRed();
                int green = color.getGreen();
                int blue = color.getBlue();
                int modifiedRGB = new Color(red, green, blue, originalColor.getAlpha()).getRGB();
                modifiedImage.setRGB(i, j, modifiedRGB);
            }
        }
        return modifiedImage;
    }
}
```
