// Selecione a imagem Sentinel-2 na data desejada e referente à cena T20NQF
var imagemSentinel2 = ee.ImageCollection('COPERNICUS/S2')
  .filterDate('2015-11-23', '2015-11-24') // Filtra para a data específica
  .filterMetadata('MGRS_TILE', 'equals', '20NQF') // Filtra pela cena T20NQF
  .sort('CLOUDY_PIXEL_PERCENTAGE') // Ordena por porcentagem de nuvens ascendente
  .first(); // Seleciona a primeira imagem (menos nuvens)

// Verifique se há uma imagem na coleção
if (imagemSentinel2) {
  // Imprimir os metadados da imagem
  print('Metadados da Imagem Sentinel-2:', imagemSentinel2.getInfo());

  // Seleciona apenas a banda 11 da imagem
  var banda11 = imagemSentinel2.select(['B11']);

  // Converta a banda para UInt16
  var banda11Uint16 = banda11.toUint16();

  // Visualize a imagem na tela
  Map.addLayer(banda11Uint16, {
    min: 0,
    max: 3000,
    palette: ['000000', 'FFFFFF'] // Ajuste a paleta de cores conforme necessário
  }, 'Sentinel-2 Band 11 - T20NQF');

  // Exporte a banda 11 para o Google Drive
  Export.image.toDrive({
    image: banda11Uint16,
    description: 'Sentinel2_Band11_T20NQF',
    scale: 20, // Reduzi a escala para diminuir o número de pixels
    region: imagemSentinel2.geometry() // Usa a geometria da imagem como região
  });
} else {
  print('Nenhuma imagem encontrada para a cena T20NQF na data especificada.');
}
