# symfony
SYMNFONY cheatsheet

START:
composer create-project symfony/website-skeleton my-project

Next:
Change directory (cd (naam) )

DB:
Change database name. Put db on. then:
php bin/console doctrine:database:create

Overige commands:
php bin/console make:controller-> om een controller met bijbehorende view te bouwen.
php bin/console make:entity-> om een entiteit te definieren, blauwdruk van een tabel in je database.
php bin/console doctrine:schema:update --force-> de database schema instellingen wegschrijven in dbase afgeleid van de entiteiten.
php bin/console make:crud-> om de crud te bouwen.

Om webpack en npm hebben als je het nodig hebt:
 composer require symfony/webpack-encore-bundle
 yarn install

Voor user security bundle:
composer require symfony/security-bundle
php bin/console make:user
php bin/console make:auth

Bootstrap:
twig(staat in config):
    default_path: '%kernel.project_dir%/templates'
    form_themes:
        - 'bootstrap_4_horizontal_layout.html.twig'

https://github.com/dompdf/dompdf
https://symfony.com/doc/2.x/bundles/EasyAdminBundle/integration/vichuploaderbundle.html
composer require easycorp/easyadmin-bundle


Voor een naf bar (verander de juiste dingen)
<nav class="sticky-top navbar navbar-expand-lg navbar-light">
    <a class="navbar-brand" href="{{ path('home') }}">
        <img class="img-fluid" src="{{ asset('images/logo_innovatiehub.svg') }}" alt="BigData">
    </a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
    </button>
    <!-- TODO: add active class based on URL -->
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav ml-auto mr-4">
            <li class="nav-item">
                <a class="nav-link active" href="{{ path('home') }}">Home <span class="sr-only">(current)</span></a>
            </li>
            <li class="nav-item disabled">
                <a class="nav-link" href="{{ path('nieuws_index') }}">Nieuws</a>
            </li>
            <li class="nav-item disabled">
                <a class="nav-link" href="{{ path('partner') }}">Partners</a>
            </li>
            <li class="nav-item disabled">
                <a class="nav-link" href="{{ path('contact') }}">Contact</a>
            </li>
        </ul>
</div>
</nav>

Easyadmin 3 config:
class DashboardController extends AbstractDashboardController
{
    /**
     * @Route("/admin", name="admin")
     * @return Response
     */
    public function index(): Response
    {
        $routeBuilder = $this->get(CrudUrlGenerator::class)->build();

        return $this->redirect($routeBuilder->setController(NewsCrudController::class)->generateUrl());
    }

    public function configureDashboard(): Dashboard
    {
        return Dashboard::new()
            ->setTitle('Titel');
    }
    public function configureMenuItems(): iterable
    {
        yield MenuItem::section('Administration');
        yield MenuItem::linktoDashboard('Dashboard', 'fa fa-home');
        yield MenuItem::linkToCrud('Users', 'fa fa-user', User::class);

    }
}

Voor een easyadmin3 crud:
php bin/console make:admin:crud

Voor pictures:
        $filename     = ImageField::new('imageName', 'File')
        ->setBasePath('images/news')
        ->setUploadDir('public/images/news');

return[
            TextField::new('title'),
            $textfield,
            BooleanField::new('frontpage'),
            TextField::new('imageName'),
            $filename
];


Met problemen met de pictures, verwijder dit in de source.
Zit in EasyAdminBundle/src/Form/Type/FileUploadType.php:


if (0 !== mb_strpos($value, \DIRECTORY_SEPARATOR)) {

$value = $this->projectDir.'/'.$value;

}



