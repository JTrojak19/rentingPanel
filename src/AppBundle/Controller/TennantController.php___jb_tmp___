<?php

namespace AppBundle\Controller;

use AppBundle\Entity\Tennant;
use Symfony\Bundle\FrameworkBundle\Controller\Controller;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Method;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;use Symfony\Component\HttpFoundation\Request;

/**
 * Tennant controller.
 *
 * @Route("tennant")
 */
class TennantController extends Controller
{
    /**
     * Lists all tennant entities.
     *
     * @Route("/", name="tennant_index")
     * @Method("GET")
     */
    public function indexAction()
    {
        $em = $this->getDoctrine()->getManager();

        $tennants = $em->getRepository('AppBundle:Tennant')->findAll();

        return $this->render('tennant/index.html.twig', array(
            'tennants' => $tennants,
        ));
    }

    /**
     * Creates a new tennant entity.
     *
     * @Route("/new", name="tennant_new")
     * @Method({"GET", "POST"})
     */
    public function newAction(Request $request)
    {
        $tennant = new Tennant();
        $form = $this->createForm('AppBundle\Form\TennantType', $tennant);
        $form->handleRequest($request);

        if ($this->countAction() < 20) {
            if ($form->isSubmitted() && $form->isValid()) {
                $em = $this->getDoctrine()->getManager();
                $em->persist($tennant);
                $em->flush();

                return $this->redirectToRoute('tennant_show', array('id' => $tennant->getId()));
            }

            return $this->render('tennant/new.html.twig', array(
                'tennant' => $tennant,
                'form' => $form->createView(),
            ));
        }
        else
        {
            return $this->redirectToRoute('tennant_index');
        }
    }
    public function countAction()
    {
        $em = $this->getDoctrine()->getManager();
        $qb = $em->createQueryBuilder();

        $qb->select('count(t.id)');
        $qb->from('AppBundle:Tennant','t');

        $count = $qb->getQuery()->getSingleScalarResult();

        return $count;
    }

    /**
     * Finds and displays a tennant entity.
     *
     * @Route("/{id}", name="tennant_show")
     * @Method("GET")
     */
    public function showAction(Tennant $tennant)
    {
        $deleteForm = $this->createDeleteForm($tennant);

        return $this->render('tennant/show.html.twig', array(
            'tennant' => $tennant,
            'delete_form' => $deleteForm->createView(),
        ));
    }

    /**
     * Displays a form to edit an existing tennant entity.
     *
     * @Route("/{id}/edit", name="tennant_edit")
     * @Method({"GET", "POST"})
     */
    public function editAction(Request $request, Tennant $tennant)
    {
        $deleteForm = $this->createDeleteForm($tennant);
        $editForm = $this->createForm('AppBundle\Form\TennantType', $tennant);
        $editForm->handleRequest($request);

        if ($editForm->isSubmitted() && $editForm->isValid()) {
            $this->getDoctrine()->getManager()->flush();

            return $this->redirectToRoute('tennant_edit', array('id' => $tennant->getId()));
        }

        return $this->render('tennant/edit.html.twig', array(
            'tennant' => $tennant,
            'edit_form' => $editForm->createView(),
            'delete_form' => $deleteForm->createView(),
        ));
    }

    /**
     * Deletes a tennant entity.
     *
     * @Route("/{id}", name="tennant_delete")
     * @Method("DELETE")
     */
    public function deleteAction(Request $request, Tennant $tennant)
    {
        $form = $this->createDeleteForm($tennant);
        $form->handleRequest($request);

        if ($form->isSubmitted() && $form->isValid()) {
            $em = $this->getDoctrine()->getManager();
            $dql = "";
        }

        //return $this->redirectToRoute('tennant_index');
    }

    /**
     * Creates a form to delete a tennant entity.
     *
     * @param Tennant $tennant The tennant entity
     *
     * @return \Symfony\Component\Form\Form The form
     */
    private function createDeleteForm(Tennant $tennant)
    {
        return $this->createFormBuilder()
            ->setAction($this->generateUrl('tennant_delete', array('id' => $tennant->getId())))
            ->setMethod('DELETE')
            ->getForm()
        ;
    }
}
